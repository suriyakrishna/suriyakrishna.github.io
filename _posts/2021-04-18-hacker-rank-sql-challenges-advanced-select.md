---
layout: post
title: Hacker Rank SQL Challenges Advanced Select
date: 2021-04-18 16:28:00 +0530
categories: hackerrank sql
---

[Hacker Rank SQL Challenges](https://www.hackerrank.com/domains/sql)

#### Problems
1. [Type of Triangle](#type-of-triangle)
1. [The PADS](#the-pads)
1. [Occupations](#occupations)
1. [Binary Tree Nodes](#binary-tree-nodes)
1. [New Companies](#new-companies)


#### Type of Triangle
> Problem -> [URL](https://www.hackerrank.com/challenges/what-type-of-triangle/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Using case statement we need to check if the given sides of triangle are Equilateral, Isosceles, Scalene or Not A Triangle.
> - Condition to check if triangle can be formed with given dimensions - SUM(A, B) greater than C 
> - Condition for Equilateral - all three sides are equal.
> - Condition for Isosceles - any two sides are equal.
> - Condition for Scalene - none of the sides are equal.
>  
> Solution:
> ```sql
> SELECT 
> CASE 
>     WHEN (A + B) <= C THEN 'Not A Triangle'
>     WHEN A = B AND B = C THEN 'Equilateral'
>     WHEN A = B OR B = C OR A = C THEN 'Isosceles'
>     WHEN A <> B AND B <> C AND A <> C THEN 'Scalene' 
> END AS type_of_triangle
> FROM triangles;
> ```


#### The PADS
> Problem -> [URL](https://www.hackerrank.com/challenges/the-pads/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> <br>
> Query 1:
> 1. Use concat and form the required string.
> 2. Order the result by `name` in ascending order.
> 
> Query 2:
> 1. Create temporary view with `occupation` and it's count.
> 2. From temporary view form the required string.
> 3. Order the result by `occupation_count` and `occupation` in ascending order.
> 
> Solution:
> ```sql
> -- QUERY 1
> SELECT name || '(' || SUBSTR(occupation, 0, 1) || ')' 
> FROM occupations 
> ORDER BY name;
> 
> -- QUERY 2
> SELECT 'There are a total of ' || t.occupation_count || ' ' || LOWER(t.occupation) || 's.' 
> FROM (
>     SELECT occupation, 
>     count(occupation) AS occupation_count 
>     FROM occupations 
>     GROUP BY occupation
> ) t
> ORDER BY t.occupation_count,
> t.occupation;
> ```


#### Occupations
> Problem -> [URL](https://www.hackerrank.com/challenges/occupations/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. Create `occupation_view` using `WITH` clause with name, occupation and row_number for each name in occupation order by name in descending order.
> 2. Create `level_view` using `CONNECT BY` clause with `LEVEL` value less than and equal to `MAX(row_num)` from occupation_view.
> 3. Using `level_view` as left table we need to join with `occupation_view` for each profession using `row_num` column.
> 4. Select `doctor.name`, `professor.name`, `singer.name` and `actor.name` from join result.
>  
> Solution:
> ```sql
> WITH occupation_view AS (
>     SELECT name, 
>     occupation, 
>     ROW_NUMBER() OVER(PARTITION BY occupation ORDER BY name) row_num 
>     FROM occupations
> ),
> level_view AS (
>     SELECT LEVEL as row_num
>     FROM DUAL 
>     CONNECT BY LEVEL <= (SELECT MAX(row_num) FROM occupation_view)
> )
> SELECT doctor.name,
> professor.name,
> singer.name,
> actor.name
> FROM level_view l
> LEFT JOIN
> (
>     SELECT name, row_num
>     FROM occupation_view
>     WHERE LOWER(occupation) = 'doctor'
> ) doctor
> ON
> l.row_num = doctor.row_num
> LEFT JOIN
> (
>     SELECT name, row_num
>     FROM occupation_view
>     WHERE LOWER(occupation) = 'professor'
> ) professor
> ON
> l.row_num = professor.row_num
> LEFT JOIN
> (
>     SELECT name, row_num
>     FROM occupation_view
>     WHERE LOWER(occupation) = 'singer'
> ) singer
> ON
> l.row_num = singer.row_num
> LEFT JOIN
> (
>     SELECT name, row_num
>     FROM occupation_view
>     WHERE LOWER(occupation) = 'actor'
> ) actor
> ON
> l.row_num = actor.row_num;
> ```


#### Binary Tree Nodes
> Problem -> [URL](https://www.hackerrank.com/challenges/binary-search-tree-1/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. Using case statement we can determine if the given node is Root, Inner or Leaf.
> - Node is said to be Root if it's parent node is null.
> - Node is said to be Inner if the node is present in parent.
> - Node is said to be Leaf if the node is either Root nor Inner(no child nodes).
> 2. Order result by node value in ascending order.
>  
> Solution:
> ```sql
> SELECT n,
> CASE
>     WHEN p IS NULL THEN 'Root'
>     WHEN n IN (SELECT DISTINCT p FROM bst) THEN 'Inner'
>     ELSE 'Leaf'
> END AS node_type
> FROM bst
> ORDER BY n;
> ```


#### New Companies
> Problem -> [URL](https://www.hackerrank.com/challenges/the-company/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. Count distinct of lead managers, senior managers, managers and employees for each `company_code` from their respective tables.
> 2. Do left join of all the count with company table using `company_code` column.
> 3. Select `company_code`, `founder`, `lead_manager_count`, `senior_manager_count`, `manager_count` and `employee_count` from join result
> 4. Order result by `company_code` in ascending order. 
> 
> Solution:
> ```sql
> SELECT c.company_code, 
> c.founder,
> lm.lead_manager_count,
> sm.senior_manager_count,
> m.manager_count,
> e.employee_count
> FROM company c
> LEFT JOIN
> (
>     SELECT company_code,
>     COUNT(DISTINCT lead_manager_code) lead_manager_count
>     FROM
>     lead_manager
>     GROUP BY
>     company_code
> ) lm
> ON 
> c.company_code = lm.company_code
> LEFT JOIN
> (
>     SELECT company_code,
>     COUNT(DISTINCT senior_manager_code) senior_manager_count
>     FROM
>     senior_manager
>     GROUP BY
>     company_code
> ) sm
> ON 
> c.company_code = sm.company_code
> LEFT JOIN
> (
>     SELECT company_code,
>     COUNT(DISTINCT manager_code) manager_count
>     FROM
>     manager
>     GROUP BY
>     company_code
> ) m
> ON 
> c.company_code = m.company_code
> LEFT JOIN
> (
>     SELECT company_code,
>     COUNT(DISTINCT employee_code) employee_count
>     FROM
>     employee
>     GROUP BY
>     company_code
> ) e
> ON 
> c.company_code = e.company_code
> ORDER BY 
> c.company_code;
> ```