---
layout: post
title: Hacker Rank SQL Challenges Basic Join
date: 2021-05-30 16:00:00 +0530
categories: hackerrank sql
---

[Hacker Rank SQL Challenges](https://www.hackerrank.com/domains/sql)

#### Problems
1. [Population Census](#population-census)
1. [African Cities](#african-cities)
1. [Average Population of Each Continent](#average-population-of-each-continent)
1. [The Report](#the-report)
1. [Top Competitors](#top-competitors)
1. [Ollivander's Inventory](#ollivanders-inventory)
1. [Challenges](#challenges)
1. [Contest Leaderboard](#contest-leaderboard)

#### Population Census
> Problem -> [URL](https://www.hackerrank.com/challenges/asian-population/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Join `city` and `country` table on `city.countrycode` equal to `country.code`.
> 2. Filter `country.continent` equal to 'asia'.
> 3. Aggregate sum of `city.population`.
>  
> Solution:
> ```sql
> SELECT SUM(ct.population) AS sum_of_population 
> FROM
> city ct
> INNER JOIN
> country cn
> ON
> ct.countrycode = cn.code
> WHERE
> LOWER(cn.continent) = 'asia';
> ```


#### African Cities
> Problem -> [URL](https://www.hackerrank.com/challenges/african-cities/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Join `city` and `country` table on `city.countrycode` equal to `country.code`.
> 2. Filter `country.continent` equal to 'africa'.
> 3. Select only `city.name`.
>  
> Solution:
> ```sql
> SELECT ct.name 
> FROM
> city ct
> INNER JOIN
> country cn
> ON
> ct.countrycode = cn.code
> WHERE
> LOWER(cn.continent) = 'africa';
> ```


#### Average Population of Each Continent
> Problem -> [URL](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Join `city` and `country` table on `city.countrycode` equal to `country.code`.
> 2. Group By `country.continent`.
> 3. Aggregate `AVG(city.population)` and `ROUND` down to nearest integer.
>  
> Solution:
> ```sql
> SELECT cn.continent, FLOOR(AVG(ct.population)) AS avg_population 
> FROM
> city ct
> INNER JOIN
> country cn
> ON
> ct.countrycode = cn.code
> GROUP BY cn.continent;
> ```


#### The Report
> Problem -> [URL](https://www.hackerrank.com/challenges/the-report/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. Join `students` and `grades` table on `students.marks` between `grades.min_mark` and `grades.max_mark`.
> 2. In select, apply case clause for `students.name`.
> 3. Order By `grades.grade` descending, `students.name` ascending and apply case clause where `grades.grade` < 8 to order the results by `students.marks`.
>  
> Solution:
> ```sql
> SELECT
> CASE
>     WHEN g.grade < 8 THEN NULL
>     ELSE s.name
> END AS name,
> g.grade,
> s.marks
> FROM 
> students s
> INNER JOIN 
> grades g
> ON
> s.marks between g.min_mark and g.max_mark
> ORDER BY g.grade DESC, s.name ASC, CASE WHEN g.grade < 8 THEN s.marks END ASC;
> ```


#### Top Competitors
> Problem -> [URL](https://www.hackerrank.com/challenges/full-score/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. Joins
> - `difficulty` table with `challenges` on `difficulty_level`.
> - `challenges` table with `submissions` on `challenge_id`.
> - `submissions` table with `hackers` on `hacker_id`.
> 2. Group by `hacker_id`, `name` having count of challenges greater than 1.
> 3. Select `hacker_id`, `name` and aggregated value for `count_of_challenges`
> 4. Select `hacker_id` and `name` from the subquery.
> 5. Order the result by `count_of_challenges` in descending and `hacker_id` in ascending order.
> 
> Solution:
> ```sql
> SELECT t.hacker_id, t.name
> FROM (
>     SELECT 
>     h.hacker_id,
>     h.name,
>     COUNT(DISTINCT s.challenge_id) AS count_of_challenges
>     FROM 
>     difficulty d
>     INNER JOIN
>     challenges c
>     ON
>     d.difficulty_level = c.difficulty_level
>     INNER JOIN
>     submissions s
>     ON
>     c.challenge_id = s.challenge_id AND s.score = d.score
>     LEFT JOIN
>     hackers h
>     ON
>     s.hacker_id = h.hacker_id 
>     GROUP BY h.hacker_id, h.name HAVING COUNT(DISTINCT s.challenge_id) > 1
> ) t 
> ORDER BY t.count_of_challenges DESC, t.hacker_id;
> ```


#### Ollivander's Inventory
> Problem -> [URL](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. Join `wands` and `wands_property` on `code`.
> 2. Filter no_evil wands, `wands_property.is_evil` equal to 0.
> 3. Assign `ROW_NUMBER()` for resultant rows `PARTITION BY wands.power, wands_property.age ORDER BY wands.coins_needed ASC`. By this way we will get minimum number of gold galleons needed to buy each non-evil wand of high power and age.
> 4. Select the id, age, coins_needed, power from sub-query and filter `row_num` equal to 1.
> 5. Order the result by `power` and `age` both in descending order.
>
> Solution:
> ```sql
> SELECT
> t.id,
> t.age,
> t.coins_needed,
> t.power
> FROM (
>     SELECT w.id, 
>     wp.age, 
>     w.coins_needed, 
>     w.power,
>     ROW_NUMBER() OVER(PARTITION BY w.power, wp.age ORDER BY w.coins_needed) AS row_num
>     FROM wands w
>     INNER JOIN
>     wands_property wp
>     ON
>     w.code = wp.code
>     WHERE
>     wp.is_evil = 0
> ) t
> WHERE t.row_num = 1
> ORDER BY t.power DESC, t.age DESC;
> ```


#### Challenges
> Problem -> [URL](https://www.hackerrank.com/challenges/challenges/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> <br>
> Create temporary view `total_challenges`,
> <br>
> 1. Join `hackers` and `challenges` on `hacker_id` column.
> 2. Select `hacker.hacker_id` and `hacker.name`.
> 3. Aggregate count of challenges for every hacker.
> 4. Group By `hacker.hacker_id` and `hacker.name`.
> 
> Create temporary view `required_ids`,
> <br>
> 1. To handle `If more than one student created the same number of challenges and the count is less than the maximum number of challenges` condition we will create a `required_ids` temporary view.
> 2. Select hacker_id from `total_challenges`.
> 3. Using case clause we will create column `required`. Condition `challenges_created` by the hacker is not equal to `max_challenges` created by hackers and `count of hackers` with same number of challenges is greater than 1 then we don't need to include those hackers in our final result. 
> 4. Basically, we will assign 1 to `required` if we want to include those hackers in our final result else 0.
> 
> Finally,
> <br>
> 1. Join `total_challenges` and `required_ids` on `hacker_id` column.
> 2. Filter `required_ids.required` equal to 1.
> 3. Select `hacker_id`, `name` and `challenges_created` from `total_challenges`.
> 4. Order the result by `total_challenges.hacker_id` in descending order and `total_challenges.hacker_id` in ascending order.
>
> Solution:
> ```sql
> WITH total_challenges AS (
>     SELECT 
>     h.hacker_id,
>     h.name,
>     COUNT(1) AS challenges_created
>     FROM 
>     hackers h
>     INNER JOIN
>     challenges c
>     ON
>     h.hacker_id = c.hacker_id
>     GROUP BY
>     h.hacker_id, h.name
> ),
> required_ids AS (
>     SELECT hacker_id,
>     CASE 
>         WHEN challenges_created != MAX(challenges_created) OVER() AND COUNT(1) OVER(PARTITION BY challenges_created) > 1 THEN 0
>         ELSE 1
>     END AS required
>     FROM
>     total_challenges
> )
> SELECT t.hacker_id,
> t.name,
> t.challenges_created
> FROM
> total_challenges t
> INNER JOIN
> required_ids r
> ON
> t.hacker_id = r.hacker_id
> WHERE r.required = 1
> ORDER BY t.challenges_created DESC, t.hacker_id;
> ```


#### Contest Leaderboard
> Problem -> [URL](https://www.hackerrank.com/challenges/contest-leaderboard/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> <br>
> Create temporary view `max_hacker_score`,
> <br>
> 1. Select `hacker_id`, `challenge_id` from submissions.
> 2. Aggregate max of score for each `hacker_id` and `challenge_id`.
> 3. Group By `hacker_id` and `challenge_id`.
> 
> Create temporary view `total_scores`,
> <br>
> 1. Join `hackers` and `max_hacker_score` on `hacker_id`.
> 2. Select `hackers.hacker_id`, `hacker.name` from `hackers`.
> 3. Aggregate sum of scores for each hacker.
> 4. Group by `hackers.hacker_id` and `hackers.name` and having sum greater than 0.
> 
> Finally,
> <br>
> 1. Select `hacker_id`, `name` and `total_score` from `total_scores`.
> 2. Order the result by `total_score` in descending order and `hacker_id` in ascending order.
> 
> Solution:
> ```sql
> WITH max_hacker_score AS (
>     SELECT hacker_id, 
>     challenge_id, 
>     max(score) AS max_score 
>     FROM submissions 
>     GROUP BY hacker_id, challenge_id
> ),
> total_scores AS (
>     SELECT h.hacker_id,
>     h.name,
>     SUM(m.max_score) AS total_score
>     FROM 
>     hackers h
>     INNER JOIN
>     max_hacker_score m
>     ON
>     h.hacker_id = m.hacker_id
>     GROUP BY h.hacker_id, h.name HAVING SUM(m.max_score) > 0
> )
> SELECT t.hacker_id,
> t.name,
> t.total_score
> FROM
> total_scores t
> ORDER BY t.total_score DESC, t.hacker_id ASC;
> ```
