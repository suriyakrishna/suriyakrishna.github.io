---
layout: shell_scripts_post
title: Shell Scripting Generic Functions
date: 2021-03-21 13:38:04 +0530
categories: shell-scripting
---

> [Shell Scripting Standards](http://ronaldbradford.com/blog/scripting-standards/)

### Logging
```bash
function log(){
    local TMS=$(date +"%m-%d-%Y %H:%M:%S")
    local LEVEL="${1^^}"
    local MESSAGE="${2}"
    echo "${TMS} - ${LEVEL} - ${MESSAGE}"
}
function log_info(){
    log " INFO" "${1}"
}

function log_error(){
    log "ERROR" "${1}"
}

function log_debug(){
    log "DEBUG" "${1}"
}
```

### e-mail 
```bash
export FROM=$(whoami)
export EMAIL_TO="xyz"
export DOMAIN=$(domainname)

function send_email(){

}
```

### Command Status Check
```bash
function command_status_check(){
    local STATUS=${?}
    local SUCCESS_MESSAGE="${1} - SUCCESS"
    local ERROR_MESSAGE="${1} - FAILED"
    if [[ "${STATUS}" == "0" ]]; then
        log_info "${SUCCESS_MESSAGE}"
    else
        log_error "${ERROR_MESSAGE}"
        exit 1
    fi
}
```

### File Exists Check
```bash
function file_exists_check(){
    local FILE_PATH=${1}
    if [[ -f ${FILE_PATH} ]]; then
        log_info "FILE EXISTS - ${FILE_PATH}"
    else
        log_error "FILE DOSEN'T EXISTS - ${FILE_PATH}"
        exit 1
    fi
}
```

### Time Elapsed
```bash
function time_elapsed(){
    local START_TIME_IN_EPOCH=${1}
    local END_TIME_IN_EPOCH=${2}
    if [[ "${START_TIME_IN_EPOCH}" == "" ]]; then
        log_error "START TIME SHOULD NOT BE EMPTY"
        return 1 
    fi
    if [[ "${END_TIME_IN_EPOCH}" == "" ]]; then
        log_error "END TIME SHOULD NOT BE EMPTY"
        return 1   
    fi
    if [[ ${END_TIME_IN_EPOCH} < ${START_TIME_IN_EPOCH} ]]; then
        log_error "END TIME SHOULD BE GREATER THAT START TIME"
        return 1
    fi
    local TOTAL_SECS=$((${END_TIME_IN_EPOCH} - ${START_TIME_IN_EPOCH}))
    local ELAPSED_SECS=$((${TOTAL_SECS} % 60))
    local ELAPSED_MINS=$(((${TOTAL_SECS} / 60) % 60))
    local ELAPSED_HOURS=$(((${TOTAL_SECS} / 3600) % 24))
    local ELAPSED_DAYS=$((${TOTAL_SECS} / 86400))
    echo "${ELAPSED_DAYS} DAYS ${ELAPSED_HOURS} HOURS ${ELAPSED_MINS} MINS ${ELAPSED_SECS} SECS"
}
```