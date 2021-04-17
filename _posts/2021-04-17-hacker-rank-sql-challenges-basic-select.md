---
layout: post
title: Hacker Rank SQL Challenges Basic Select
date: 2021-04-17 13:46:00 +0530
categories: hackerrank sql
---

[Hacker Rank SQL Challenges](https://www.hackerrank.com/domains/sql)

#### Revising the Select Query I
> Problem -> [URL](https://www.hackerrank.com/challenges/revising-the-select-query/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode:
> 1. Select `all` fields. 
> 2. Filter `countrycode` equal to 'USA' `Casting the string value either to upper or lower case for comparision will be best approach` and `population` greater than 100000
>  
> Solution:
> ```sql
> SELECT * FROM city 
> WHERE population > 100000 AND UPPER(countrycode) = 'USA';
> ```


#### Revising the Select Query II
> Problem -> [URL](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `name` field.
> 1. Filter `countrycode` equal to 'USA' `Casting the string value either to upper or lower case for comparision will be best approach` and `population` greater than 120000
>  
> Solution:
> ```sql
> SELECT name FROM city 
> WHERE population > 120000 AND UPPER(countrycode) = 'USA';
> ```


#### Select All
> Problem -> [URL](https://www.hackerrank.com/challenges/select-all-sql/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `all` fields and return `all` rows.
>  
> Solution:
> ```sql
> SELECT * FROM city;
> ```


#### Select By ID
> Problem -> [URL](https://www.hackerrank.com/challenges/select-by-id/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `all` fields.
> 2. Filter `id` equal to 1661.
>  
> Solution:
> ```sql
> SELECT * FROM city 
> WHERE id = 1661;
> ```


#### Japanese Cities' Attributes
> Problem -> [URL](https://www.hackerrank.com/challenges/japanese-cities-attributes/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `all` fields.
> 2. Filter `countrycode` equal to 'JPN'.
>  
> Solution:
> ```sql
> SELECT * FROM city 
> WHERE UPPER(countrycode) = 'JPN';
> ```


#### Japanese Cities' Names
> Problem -> [URL](https://www.hackerrank.com/challenges/japanese-cities-name/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `name` field.
> 2. Filter `countrycode` equal to 'JPN'.
>  
> Solution:
> ```sql
> SELECT name FROM city 
> WHERE UPPER(countrycode) = 'JPN';
> ```


#### Weather Observation Station 1
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-1/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `city` and `state` field.
>  
> Solution:
> ```sql
> SELECT city, state FROM station;
> ```


#### Weather Observation Station 2
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-2/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select sum of `LAT_N` field and sum of `LONG_W` field round upto 2 decimal.
>  
> Solution:
> ```sql
> SELECT ROUND(SUM(LAT_N),2), ROUND(SUM(LONG_W),2) FROM station;
> ```


#### Weather Observation Station 3
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-3/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter even `id` values.
> 3. Return distinct `city` names. `Best approach is to go with GROUP BY instead of DISTINCT. GROUP BY performs better than DISTINCT.` 
>  
> Solution:
> ```sql
> SELECT city FROM station
> WHERE MOD(id,2) = 0
> GROUP BY city;
> ```


#### Weather Observation Station 4
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-4/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select count of cities.
> 2. Select count of distinct cities.
> 3. Find difference of both.
>  
> Solution:
> ```sql
> SELECT (SELECT COUNT(city) c FROM station) - (SELECT COUNT(DISTINCT city) dc FROM station) FROM dual;
> ```


#### Weather Observation Station 5
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-5/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Create a temporary view using `WITH` clause which will contains `city`, length for each `city` and row_num when we order each length by `city` 
> 2. Select city and length of city from temporary view.
>     - Filter city_length is in (max length from temporary view and min length from temporary view) and row_num = 1
>  
> Solution:
> ```sql
> WITH city_name_with_length AS (
>     SELECT city, 
>     LENGTH(city) AS city_length, 
>     ROW_NUMBER() OVER (PARTITION BY LENGTH(city) ORDER BY city) AS row_num 
>     FROM station
> )
> SELECT city, city_length 
> FROM city_name_with_length 
> WHERE city_length in (
>     (SELECT MIN(city_length) FROM  city_name_with_length), 
>     (SELECT MAX(city_length) FROM  city_name_with_length)
> ) AND row_num = 1;
> ```


#### Weather Observation Station 6
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-6/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter using `REGEX_LIKE` function `city` name starts with vowels.
> 3. Return distinct `city` names. 
>  
> Solution:
> ```sql
> SELECT city FROM station 
> WHERE REGEXP_LIKE(LOWER(city), '^[aeiou]')
> GROUP BY city;
> ```


#### Weather Observation Station 7
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-7/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter using `REGEX_LIKE` function `city` name ends with vowels.
> 3. Return distinct `city` names.
>  
> Solution:
> ```sql
> SELECT city FROM station 
> WHERE REGEXP_LIKE(LOWER(city), '.[aeiou]$')
> GROUP BY city;
> ```


#### Weather Observation Station 8
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-8/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter using `REGEX_LIKE` function `city` name starts and ends with vowels.
> 3. Return distinct `city` names. 
>  
> Solution:
> ```sql
> SELECT city FROM station 
> WHERE REGEXP_LIKE(city, '^[aeiou][a-z ]*?[aeiou]$', 'i') 
> GROUP BY city;
> ```


#### Weather Observation Station 9
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-9/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter using `REGEX_LIKE` function `city` name doesn't starts with vowels.
> 3. Return distinct `city` names.
>  
> Solution:
> ```sql
> SELECT city FROM station 
> WHERE REGEXP_LIKE(LOWER(city), '^[^aeiou]')
> GROUP BY city;
> ```


#### Weather Observation Station 10
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-10/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter using `REGEX_LIKE` function `city` name doesn't end with vowels.
> 3. Return distinct `city` names.
>  
> Solution:
> ```sql
> SELECT city FROM station 
> WHERE REGEXP_LIKE(LOWER(city), '.[^aeiou]$')
> GROUP BY city;
> ```


#### Weather Observation Station 11
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-11/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter using `REGEX_LIKE` function `city` name doesn't starts or ends with vowels.
> 3. Return distinct `city` names.
>  
> Solution:
> ```sql
> SELECT city FROM station 
> WHERE REGEXP_LIKE(city, '^[^aeiou].|.[^aeiou]$', 'i') 
> GROUP BY city;
> ```


#### Weather Observation Station 12
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-12/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `city` field.
> 2. Filter using `REGEX_LIKE` function `city` name doesn't starts and ends with vowels.
> 3. Return distinct `city` names.
>  
> Solution:
> ```sql
> SELECT city FROM station 
> WHERE REGEXP_LIKE(city, '^[^aeiou][a-z ]*?[^aeiou]$', 'i') 
> GROUP BY city;
> ```


#### Higher Than 75 Marks
> Problem -> [URL](https://www.hackerrank.com/challenges/more-than-75-marks/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `name` field.
> 2. Filter `marks` greater than 75.
> 3. Order the result by last three character of each `name` (we need to use substring to get last three character) in ascending order and secondary sort by `id` in ascending order.
>  
> Solution:
> ```sql
> SELECT name FROM students 
> WHERE marks > 75
> ORDER BY SUBSTR(name, (LENGTH(name) - 2), 3), id;
> ```


#### Employee Names
> Problem -> [URL](https://www.hackerrank.com/challenges/name-of-employees/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `name` field.
> 2. Order the result by `name` in ascending order.
>  
> Solution:
> ```sql
> SELECT name FROM employee
> ORDER BY name;
> ```


#### Employee Salaries
> Problem -> [URL](https://www.hackerrank.com/challenges/salary-of-employees/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select only `name` field.
> 2. Filter `salary` greater than $2000/month (Salary in `salary` field is salary/month) and `months` less than 10
> 2. Order the result by `employee_id` ascending order.
>  
> Solution:
> ```sql
> SELECT name FROM employee
> WHERE salary > 2000 AND months < 10
> ORDER BY employee_id;
> ```