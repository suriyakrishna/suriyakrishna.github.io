---
layout: post
title: Hacker Rank SQL Challenges Advanced Join
date: 2021-06-12 14:53:00 +0530
categories: hackerrank sql
---

[Hacker Rank SQL Challenges](https://www.hackerrank.com/domains/sql)

#### Problems
1. [SQL Project Planning](#sql-project-planning)
1. [Placements](#placements)
1. [Symmetric Pairs](#symmetric-pairs)
1. [Interviews](#interviews)
1. [15 Days of Learning SQL](#15-days-of-learning-sql)


#### SQL Project Planning
> Problem -> [URL](https://www.hackerrank.com/challenges/sql-projects/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> <br>
>  <i>If task `start_date` not in `end_date` then task `start_date` will be considered as project `start_date` and similary the if task `end_date` not in `start_date` then it will be considered project `end_date`.</i>
> <i>New project will not be started until existing project completes.</i>
> <br>
> 1. We will find all the projects `start_date` and assign `row_number` to it.
> 2. We will find all the projects `end_date` and assign `row_number` to it.
> 3. Join result of step-1 and step-2 on `row_num` column.
> 4. Order the result by `end_date` - `start_date` and `start_date` in ascending order.
> 
> Solution:
> ```sql
> WITH project_start AS (
>     SELECT 
>     start_date,
>     ROW_NUMBER() OVER(ORDER BY start_date) AS row_num
>     FROM 
>     projects
>     WHERE start_date NOT IN (
>         SELECT 
>         end_date
>         FROM 
>         projects
>         GROUP BY end_date
>     )
> ),
> project_end AS (
>     SELECT 
>     end_date,
>     ROW_NUMBER() OVER(ORDER BY start_date) AS row_num
>     FROM 
>     projects
>     WHERE end_date NOT IN (
>         SELECT 
>         start_date
>         FROM 
>         projects
>         GROUP BY start_date
>     )
> )
> SELECT
> s.start_date,
> e.end_date
> FROM
> project_start s
> INNER JOIN 
> project_end e
> ON
> s.row_num = e.row_num
> ORDER BY e.end_date - s.start_date, s.start_date;
> ```


#### Placements
> Problem -> [URL](https://www.hackerrank.com/challenges/placements/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. Join `friends` with `packages` on `id` column to get the student salary.
> 2. Join `friends` with `packages` on `f.friend_id = p.id` to get the student best friend salary.
> 3. Apply filter friend_salary greater than student_salary.
> 4. Join the `result` with `students` on `id` to get the name of the student.
> 5. Order the `result` by `friend_salary`.
> 
> Solution:
> ```sql
> WITH ids AS (
>     SELECT f.id,
>     f.friend_id,
>     student_package.salary as student_salary,
>     friend_package.salary as friend_salary
>     FROM
>     friends f
>     INNER JOIN
>     packages student_package
>     ON
>     f.id = student_package.id
>     INNER JOIN
>     packages friend_package
>     ON
>     f.friend_id = friend_package.id 
>     WHERE friend_package.salary > student_package.salary
> )
> SELECT s.name
> FROM 
> students s
> INNER JOIN 
> ids i
> ON
> s.id = i.id
> ORDER BY i.friend_salary;
> ```


#### Symmetric Pairs
> Problem -> [URL](https://www.hackerrank.com/challenges/symmetric-pairs/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. We will assign row number for each row. So, while joining records we will not join records with same row number.
> 2. Perform non equi self join with symmetric pair condition and `t1.row_num != t2.row_num`
> 3. We should only return rows `x <= y` appling filter condition `x <= y`.
> 4. Remove duplicates by applying `GROUP BY x, y`
> 5. Order the `result` by `x`.
>  
> Solution:
> ```sql
> WITH pairs AS (
>     SELECT x, y, ROW_NUMBER() OVER(ORDER BY 1) row_num
>     FROM
>     functions
> )
> SELECT
> t1.x,
> t1.y
> FROM
> pairs t1
> INNER JOIN
> pairs t2
> ON
> t1.x = t2.y AND t2.x = t1.y AND t1.row_num != t2.row_num
> WHERE t1.x <= t1.y
> GROUP BY t1.x, t1.y
> ORDER BY t1.x;
> ```


#### Interviews
> Problem -> [URL](https://www.hackerrank.com/challenges/interviews/problem)
> <br>
> Difficulty Level: Hard
> <br>
> Pseudocode: 
> <br>
> <b>sum_of_views on college_id</b>
> 1. Join `challenges` with `views_stats` on `challenge_id`.
> 2. GROUP BY `college_id`.
> 3. Aggregate `SUM` of `total_views` and `total_unique_views`.
> <br>
> 
> <b>sum_of_submissions on college_id</b>
> 1. Join `challenges` with `submission_stats` on `challenge_id`.
> 2. GROUP BY `college_id`.
> 3. Aggregate `SUM` of `total_submissions` and `total_accepted_submissions`.
> <br>
> 
> <b>contest_sum on contest_id</b>
> 1. Join `colleges` with `sum_of_views` on `college_id`.
> 2. Join `colleges` with `sum_of_submissions` on `college_id`.
> 2. GROUP BY `contest_id`.
> 3. Aggregate `SUM` of `total_views`, `total_unique_views`, `total_submissions` and `total_accepted_submissions`.
> <br>
> 
> <b>result</b>
> 1. Join `contests` with `contest_sum` on `contest_id`.
> 2. Apply filter sum of `total_submissions_sum`, `total_accepted_submissions_sum`, `total_views_sum` and `total_unique_views_sum` not equal to 0.
> 3. Order the result by `contest_id`.
> 
> Solution:
> ```sql
> WITH sum_of_views AS (
>     SELECT 
>     ch.college_id,
>     SUM(vs.total_views) AS total_views_sum,
>     SUM(vs.total_unique_views) AS total_unique_views_sum
>     FROM 
>     challenges ch
>     INNER JOIN
>     view_stats vs
>     ON
>     ch.challenge_id = vs.challenge_id
>     GROUP BY ch.college_id
> ),
> sum_of_submissions AS (
>     SELECT 
>     ch.college_id,
>     SUM(ss.total_submissions) AS total_submissions_sum,
>     SUM(ss.total_accepted_submissions) AS total_accepted_submissions_sum
>     FROM 
>     challenges ch
>     INNER JOIN
>     submission_stats ss
>     ON
>     ch.challenge_id = ss.challenge_id
>     GROUP BY ch.college_id
> ),
> contest_sum AS (
>     SELECT ch.contest_id,
>     SUM(ss.total_submissions_sum) AS total_submissions_sum,
>     SUM(ss.total_accepted_submissions_sum) AS total_accepted_submissions_sum,
>     SUM(sv.total_views_sum) AS total_views_sum,
>     SUM(sv.total_unique_views_sum) AS total_unique_views_sum
>     FROM
>     colleges ch
>     INNER JOIN
>     sum_of_views sv
>     ON 
>     ch.college_id = sv.college_id
>     INNER JOIN
>     sum_of_submissions ss
>     ON
>     ch.college_id = ss.college_id
>     GROUP BY ch.contest_id
> ),
> result AS (
>     SELECT 
>     cn.contest_id,
>     cn.hacker_id,
>     cn.name,
>     cs.total_submissions_sum,
>     cs.total_accepted_submissions_sum,
>     cs.total_views_sum,
>     cs.total_unique_views_sum
>     FROM
>     contests cn
>     INNER JOIN
>     contest_sum cs
>     ON
>     cn.contest_id = cs.contest_id
>     WHERE total_submissions_sum + total_accepted_submissions_sum + total_views_sum + total_unique_views_sum <> 0
>     ORDER BY cn.contest_id
> )
> SELECT * FROM result;
> ```


#### 15 Days of Learning SQL
> Problem -> [URL](https://www.hackerrank.com/challenges/15-days-of-learning-sql/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 
> > <b>Finding unique hackers who submitted for consecutive days</b>
> > <br>
> > - <b>submissions_rank</b>
> > 1. We will assign `RANK` for each day using `DENSE_RANK` analytical function by ordering the dataset by `submission_date`.
> > 2. We will assign `RANK` for hacker's each day submission using `DENSE_RANK` analytical function Partitioning the dataset by `hacker_id` and ordering the partitioned dataset by `submission_date`.
> > 3. By assiging `RANK` we will get know if the hacker has submitted for consecutive days.
> > <br>
> > - <b>total_unique_hackers</b>
> > 1. From `submissions_rank`, If the `current_day` and hacker's consecutive days `days_submitted` rank matches then we will consider those `hacker_id` to be included in our count.
> > 2. Apply filter, `current_day` equal to `days_submitted`.
> > 3. GROUP BY `submission_date`.
> > 4. Aggregate, Count distinct of `hacker_id`.
> <br>
>
> > <b>Finding hacker_id with highest submission for each day</b>
> > - <b>hacker_submission_count</b>
> > 1. From `submissions`, Select `submission_date` and `hacker_id`.
> > 2. GROUP BY `submission_date` and `hacker_id`.
> > 3. Aggregate, count distinct of `submission_id`.
> > <br>
> > - <b>with_highest_submissions</b>
> > 1. From `hacker_submission_count`, we will assign `ROW_NUMBER` using `ROW_NUMBER` analytical function by partitioning the dataset by `submission_date` order the partitioned dataset by `submission_count` in descending and `hacker_id` in ascending order.
>
> > <b>Result</b>
> > 1. Join `total_unique_hackers` with `with_highest_submissions` on `submission_date`.
> > 2. Join `with_highest_submissions` with `hackers` on `hacker_id` to get the name of the hacker.
> > 3. Filter, `row_num` equal to 1 to get only the hackers with highest per day submissions.
> > 4. Order the result by `submission_date`.
>
> Solution:
> ```sql
> WITH submissions_rank AS (
>     SELECT submission_date,
>     hacker_id,
>     DENSE_RANK() OVER(ORDER BY submission_date) AS current_day,
>     DENSE_RANK() OVER(PARTITION BY hacker_id ORDER BY submission_date) AS days_submitted
>     FROM
>     submissions
> ),
> total_unique_hackers AS (
>     SELECT 
>     submission_date,
>     COUNT(DISTINCT hacker_id) AS distinct_hacker_count
>     FROM
>     submissions_rank
>     WHERE current_day = days_submitted
>     GROUP BY submission_date
> ),
> hacker_submission_count AS (
>     SELECT submission_date,
>     hacker_id,
>     COUNT(DISTINCT submission_id) AS submission_count
>     FROM
>     submissions
>     GROUP BY submission_date, hacker_id
> ),
> with_highest_submissions AS (
>     SELECT submission_date,
>     hacker_id,
>     ROW_NUMBER() OVER(PARTITION BY submission_date ORDER BY submission_count DESC, hacker_id ASC) AS row_num
>     FROM
>     hacker_submission_count
> ),
> result AS (
>     SELECT uh.submission_date,
>     uh.distinct_hacker_count,
>     hs.hacker_id,
>     h.name
>     FROM
>     total_unique_hackers uh
>     INNER JOIN
>     with_highest_submissions hs
>     ON
>     uh.submission_date = hs.submission_date
>     INNER JOIN
>     hackers h
>     on
>     hs.hacker_id = h.hacker_id
>     WHERE hs.row_num = 1
>     ORDER BY uh.submission_date
> )
> SELECT * FROM result;
> ```