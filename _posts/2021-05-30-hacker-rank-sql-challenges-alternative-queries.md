---
layout: post
title: Hacker Rank SQL Challenges Alternative Queries
date: 2021-05-30 18:31:00 +0530
categories: hackerrank sql
---

[Hacker Rank SQL Challenges](https://www.hackerrank.com/domains/sql)

#### Problems
1. [Draw The Triangle 1](#draw-the-triangle-1)
1. [Draw The Triangle 2](#draw-the-triangle-2)
1. [Print Prime Numbers](#print-prime-numbers)


#### Draw The Triangle 1
> Problem -> [URL](https://www.hackerrank.com/challenges/draw-the-triangle-1/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Using `LPAD` we can draw the required pattern.
> 2. Using `CONNECT BY` clause we will create 20 rows in the results.
> 3. Using Oracle's default `ROWNUM` we will order the result in descending order.
>  
> Solution:
> ```sql
> SELECT 
> LPAD('*', LEVEL * 2, ' *') AS my_string 
> FROM 
> DUAL 
> CONNECT BY LEVEL <= 20
> ORDER BY ROWNUM DESC;
> ```


#### Draw The Triangle 2
> Problem -> [URL](https://www.hackerrank.com/challenges/draw-the-triangle-2/problem)
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode: 
> 1. Using `LPAD` we can draw the required pattern.
> 2. Using `CONNECT BY` clause we will create 20 rows in the results.
>  
> Solution:
> ```sql
> SELECT 
> LPAD('*', LEVEL * 2, ' *') AS my_string 
> FROM 
> DUAL 
> CONNECT BY LEVEL <= 20;
> ```


#### Print Prime Numbers
> Problem -> [URL](https://www.hackerrank.com/challenges/print-prime-numbers/problem)
> <br>
> Difficulty Level: Medium
> <br>
> Pseudocode: 
> 1. We will create a new function `IS_PRIME` to determine if a give number is prime or not.
>     - If Number is less than or equal to 1, then the number is not prime.
>     - If Number is 2, then it it prime.
>     - If Number is greater than 2, we will iterate through a loop starting from 2 until number and we will check if the number is divisible by any of the number other than itself. If the number is divible then it will not be prime.
> 2. We will use `CONNECT BY` clause to generate 1000 rows and we check if the number is prime or not using `IS_PRIME` function.
> 3. Finally, we will use `LIST_AGG` function to print the result in required pattern.
>
> ```python
> # Prime Number Function in Python 
> # Note: This is not optimized. Brute Force Solution.
> def isPrime(n):
>     if(n <= 1):
>         return False
>     elif(n == 2):
>         return True
>     for i in range(2, n + 1):
>         if (n != i and n % i == 0):
>             return False
>     return True
> ```
>
> Solution:
> ```sql
> CREATE OR REPLACE FUNCTION IS_PRIME(num IN NUMBER) 
>    RETURN NUMBER 
>    IS bool NUMBER;
> BEGIN
>     IF(num <= 1) THEN
>         RETURN 0;
>     ELSIF(num = 2) THEN
>         RETURN 1;
>     END IF;
>     FOR i IN REVERSE 2..num LOOP
>         IF(num != i AND MOD(num,i) = 0) THEN
>             RETURN 0;
>         END IF;
>     END LOOP;
>     RETURN 1;
> END;
> /
> 
> SELECT LISTAGG(LEVEL, '&') WITHIN GROUP(ORDER BY LEVEL) AS primes 
> FROM DUAL 
> WHERE IS_PRIME(LEVEL) = 1
> CONNECT BY LEVEL <= 1000;
> ```