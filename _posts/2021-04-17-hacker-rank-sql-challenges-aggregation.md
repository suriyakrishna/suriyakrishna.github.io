---
layout: post
title: Hacker Rank SQL Challenges Aggregation
date: 2021-04-18 18:38:00 +0530
categories: hackerrank sql
---

[Hacker Rank SQL Challenges](https://www.hackerrank.com/domains/sql)

#### Revising Aggregations - The Count Function
> Problem -> [URL](https://www.hackerrank.com/challenges/revising-aggregations-the-count-function/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `COUNT(name)` from city.
> 2. Filter population greater than 100000.
>  
> Solution:
> ```sql
> SELECT COUNT(name) FROM city
> WHERE population > 100000;
> ```


#### Revising Aggregations - The Sum Function
> Problem -> [URL](https://www.hackerrank.com/challenges/revising-aggregations-sum/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `SUM(population)` from city.
> 2. Filter district equal to  'california'.
>  
> Solution:
> ```sql
> SELECT SUM(population) FROM city
> WHERE LOWER(district) = 'california';
> ```


#### Revising Aggregations - Averages
> Problem -> [URL](https://www.hackerrank.com/challenges/revising-aggregations-the-average-function/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `AVG(population)` from city.
> 2. Filter district equal to 'california'.
>  
> Solution:
> ```sql
> SELECT AVG(population) FROM city
> WHERE LOWER(district) = 'california';
> ```


#### Average Population
> Problem -> [URL](https://www.hackerrank.com/challenges/average-population/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `AVG(population)` from city and round the value using `ROUND` function.
>  
> Solution:
> ```sql
> SELECT ROUND(AVG(population)) FROM city;
> ```


#### Japan Population
> Problem -> [URL](https://www.hackerrank.com/challenges/japan-population/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `SUM(population)` from city.
> 2. Filter `countrycode` equal to 'JPN'.
>  
> Solution:
> ```sql
> SELECT SUM(population) FROM city
> WHERE UPPER(countrycode) = 'JPN';
> ```


#### Population Density Difference
> Problem -> [URL](https://www.hackerrank.com/challenges/population-density-difference/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select difference `MAX(population)` and `MIN(population)` from city.
>  
> Solution:
> ```sql
> SELECT MAX(population) - MIN(population) FROM city;
> ```


#### The Blunder
> Problem -> [URL](https://www.hackerrank.com/challenges/the-blunder/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select difference `AVG(salary)` and `AVG(REGEXP_REPLACE(salary, '[0]'))` from employees and using `CEIL` function round the result to next integer.
>  
> Solution:
> ```sql
> SELECT CEIL(AVG(salary) - AVG(REGEXP_REPLACE(salary, '[0]'))) FROM employees;
> ```


#### Top Earners
> Problem -> [URL](https://www.hackerrank.com/challenges/earnings-of-employees/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select product of months and salary and count of distinct employee_id.
> 2. Group by product of months and salary
> 3. Filter product of months and salary equal to `MAX(product of months and salary)` from employee table.
>  
> Solution:
> ```sql
> SELECT months * salary, 
> COUNT(DISTINCT employee_id) 
> FROM employee
> GROUP BY months * salary 
> HAVING months * salary = (SELECT MAX(months * salary) FROM employee);
> ```


#### Weather Observation Station 2
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-2/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select sum of `lat_n` field and sum of `long_w` field `ROUND` upto 2 decimal.
>  
> Solution:
> ```sql
> SELECT ROUND(SUM(lat_n),2), ROUND(SUM(long_w),2) FROM station;
> ```


#### Weather Observation Station 13
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-13/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select sum of `lat_n` field and `ROUND` upto 4 digits.
> 2. Filter `lat_n` BETWEEN 38.7880 and 137.2345
>  
> Solution:
> ```sql
> SELECT ROUND(SUM(lat_n),4) FROM station
> WHERE lat_n BETWEEN 38.7880 AND 137.2345;
> ```


#### Weather Observation Station 14
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-14/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select max of `lat_n` field and `ROUND` upto 4 digits.
> 2. Filter `lat_n` less than 137.2345
>  
> Solution:
> ```sql
> SELECT ROUND(MAX(lat_n),4) FROM station
> WHERE lat_n < 137.2345;
> ```


#### Weather Observation Station 15
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-15/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `long_w` field and `ROUND` upto 4 digits.
> 2. Filter `lat_n` equal to (`MAX(lat_n)` FROM station FILTER `lat_n` less than 137.2345)
>  
> Solution:
> ```sql
> SELECT ROUND(long_w,4) FROM station
> WHERE lat_n = (SELECT MAX(lat_n) FROM station WHERE lat_n < 137.2345);
> ```


#### Weather Observation Station 16
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-16/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select min of `lat_n` field and `ROUND` upto 4 digits.
> 2. Filter `lat_n` greater than 38.7780.
>  
> Solution:
> ```sql
> SELECT ROUND(MIN(lat_n),4) FROM station
> WHERE lat_n > 38.7780;
> ```


#### Weather Observation Station 17
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-17/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Select `long_w` field and `ROUND` upto 4 digits.
> 2. Filter `lat_n` equal to (`MIN(lat_n)` FROM station FILTER `lat_n` greater than 38.7780)
>  
> Solution:
> ```sql
> SELECT ROUND(long_w,4) FROM station
> WHERE lat_n = (SELECT MIN(lat_n) FROM station WHERE lat_n > 38.7780);
> ```


#### Weather Observation Station 18
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-18/problem)
> <br>
> Difficulty Level: Medium
> <br>
> <br>
> Refer [Manhattan Distance](https://xlinux.nist.gov/dads/HTML/manhattanDistance.html)
> <br>
> Pseudocode: 
> 1. Calculate `Manhattan Distance` using the formula and `ROUND` the result upto 4 digits.
>  
> Solution:
> ```sql
> SELECT ROUND(ABS(MIN(lat_n) - MAX(lat_n)) + ABS(MIN(long_w) - MAX(long_w)), 4) 
> FROM station;
> ```


#### Weather Observation Station 19
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-19/problem)
> <br>
> Difficulty Level: Medium
> <br>
> <br>
> Refer [Euclidean Distance](https://en.wikipedia.org/wiki/Euclidean_distance)
> <br>
> Pseudocode: 
> 1. Calculate `Euclidean Distance` using the formula and `ROUND` the result upto 4 digits.
>  
> Solution:
> ```sql
> SELECT ROUND(SQRT(POWER((MIN(lat_n))-MAX(lat_n),2) + POWER((MIN(long_w)-MAX(long_w)),2)), 4) 
> FROM station;
> ```


#### Weather Observation Station 20
> Problem -> [URL](https://www.hackerrank.com/challenges/weather-observation-station-20/problem)
> <br>
> Difficulty Level: Medium
> <br>
> <br>
> Refer [Median](https://en.wikipedia.org/wiki/Median)
> <br>
> Pseudocode: 
> 1. Calculate `Median` using the formula and `ROUND` the result upto 4 digits.
>  
> Solution:
> ```sql
> SELECT ROUND(MEDIAN(lat_n), 4) FROM station;
> ```