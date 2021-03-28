---
layout: shell_scripts_post
title: Shell Scripting YAML Configuration
date: 2021-03-28 12:59:04 +0530
categories: shell-scripting
---

> [Shell Scripting YAML parser github gist thread](https://gist.github.com/pkuczynski/8665367)

With the below approach, we will be able to create and support all the bash environmental variables from a single YAML file. By calling `parse_yaml.sh` with the `sample.yml` file the variables will be made available in the execution environment and we can further leverage it by creating common `env_config.sh` and we can source it as a single script wherever environment variables are required. This yaml parser works well with yaml files with 2 spaces and if we want to use with 4 spaces we need to update the `indent = length($1)/2` with `indent = length($1)/7`. If this parser is used with yaml files with 4 spaces without any changes a extra underscore will be appended for each level.

> `get_yaml_value` function accept the yaml path `ROOT_LEVEL1_LEVEL2` which can be soft or hard corded.
> 
> ```bash
> source parse_yaml.sh sample.yml
> 
> HARD_CODED=$(get_yaml_value "DEV_HIVE_DATABASE_DIR")
> 
> MY_ENV="DEV"
> SOFT_CODED=$(get_yaml_value "${MY_ENV}_HIVE_DATABASE_DIR")
> 
> echo "SOFT CODED: ${SOFT_CODED}"
> echo "HARD CODED: ${HARD_CODED}"
>
> # Console Output
> # SOFT CODED: /data/hdfs/dev/database_dev/
> # HARD CODED: /data/hdfs/dev/database_dev/
> ```

### YAML Parser - parse_yaml.sh
```bash
#!/bin/sh
function parse_yaml() {
   local prefix=$2
   local s='[[:space:]]*' w='[a-zA-Z0-9_]*' fs=$(echo @|tr @ '\034')
   sed -ne "s|^\($s\)\($w\)$s:$s\"\(.*\)\"$s\$|\1$fs\2$fs\3|p" \
        -e "s|^\($s\)\($w\)$s:$s\(.*\)$s\$|\1$fs\2$fs\3|p"  $1 |
   awk -F$fs '{
      indent = length($1)/2; 
      vname[indent] = $2;
      for (i in vname) {if (i > indent) {delete vname[i]}}
      if (length($3) > 0) {
         vn=""; for (i=0; i<indent; i++) {vn=(vn)(vname[i])("_")}
         printf("%s%s%s=\"%s\"\n", "'$prefix'",vn, $2, $3);
      }
   }'
}

function get_yaml_value(){
    local YAML_PATH=$(eval echo ${1})
    local VALUE=$(eval echo "$"$(echo ${YAML_PATH}))
    echo ${VALUE}
}

export -f get_yaml_value

YAML_PARSER_SCRIPT=$(basename $(readlink -f "${BASH_SOURCE[0]}") | cut -d"." -f1)

YAML_FILE=${1}
CONFIG_PREFIX=${2}

if [ "${YAML_FILE}" == "" ]; then
    echo "ERROR: Missing required parameter. Exiting.."
    echo "USAGE: ${YAML_PARSER_SCRIPT}.sh yaml_file.yml [config_prefix]"
    return 1
fi

if ! [ -f ${YAML_FILE} ]; then
    echo "ERROR: Yaml File Doesn't exists. Exiting.."
    return 1
fi

eval $(parse_yaml ${YAML_FILE} ${CONFIG_PREFIX})
```

### Sample YAML - sample.yml
```yml
DEV:
  HIVE_DATABASE_DIR: /data/hdfs/dev/database_dev/
  HIVE_DATABASE: database_dev
SIT:
  HIVE_DATABASE_DIR: /data/hdfs/sit/database_sit/
  HIVE_DATABASE: database_sit
PROD:
  HIVE_DATABASE_DIR: /data/hdfs/prod/database_prod/
  HIVE_DATABASE: database_prod
```

### CONFIG FILE - env_config.sh
```bash
#!/bin/sh
ENV_CONFIG_SCRIPT=$(basename $(readlink -f "${BASH_SOURCE[0]}") | cut -d"." -f1)
CONFIG_ENV=${1}
DEBUG=${2^^}

if [[ "${CONFIG_ENV}" == "" ]]; then
    echo "ERROR: Missing Required Parameter. Exiting.."
    echo "USAGE: source ${ENV_CONFIG_SCRIPT}.sh CONFIG_ENV [DEBUG]"
    return 1
fi

ENV_CONFIG_YAML="sample.yml"

source parse_yaml.sh ${ENV_CONFIG_YAML}
if [[ "$?" == "1" ]]; then
    echo "ERROR: Sourcing ${ENV_CONFIG_YAML} Failed. Exiting.."
    return 1
fi

export HIVE_DATABASE_DIR=$(get_yaml_value "${CONFIG_ENV}_HIVE_DATABASE_DIR")
export HIVE_DATABASE=$(get_yaml_value "${CONFIG_ENV}_HIVE_DATABASE")

if [[ "${DEBUG}" == "DEBUG" ]]; then
    echo "##################################################################"
    echo "~~~~~~~~~~~~~~~~~~~~~~ PARSED CONFIGURATION ~~~~~~~~~~~~~~~~~~~~~~"
    echo "##################################################################"
    echo "HIVE_DATABASE_DIR     ===> ${HIVE_DATABASE_DIR}"
    echo "HIVE_DATABASE         ===> ${HIVE_DATABASE}"
    echo "##################################################################"
fi
```

### Usage
```bash
# Using without debug
source env_config.sh DEV

# Using with debug option will prints the parsed value in console
source env_config.sh DEV debug

# Console Output:
# ##################################################################
# ~~~~~~~~~~~~~~~~~~~~~~ PARSED CONFIGURATION ~~~~~~~~~~~~~~~~~~~~~~
# ##################################################################
# HIVE_DATABASE_DIR     ===> /data/hdfs/dev/database_dev/
# HIVE_DATABASE         ===> database_dev
# ##################################################################
```

