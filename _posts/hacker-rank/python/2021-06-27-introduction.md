---
layout: post
title: Hacker Rank - Python Introduction
date: 2021-06-27 12:46:00 +0530
categories: hackerrank python
---

[Hacker Rank Python Challenges](https://www.hackerrank.com/domains/python)

***Python Version 3***

#### Problems
1. [Say "Hello, World!" With Python](#say-hello-world-with-python)
1. [Python If-Else](#python-if-else)
1. [Arithmetic Operators](#arithmetic-operators)
1. [Python: Division](#python-division)
1. [Loops](#loops)
1. [Write a function](#write-a-function)
1. [Print function](#print-function)


#### Say "Hello, World!" With Python
> Problem -> [URL](https://www.hackerrank.com/challenges/py-hello-world/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Print the required string.
>  
> Solution:
> ```python
> print("Hello, World!")
> ```


#### Python If-Else
> Problem -> [URL](https://www.hackerrank.com/challenges/py-if-else/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Validate user input, constraints `1 <= n <= 100`.
> 3. Print Weird if number is odd.
> 4. Else, If number is between 6 and 20 inclusive then print Weird, else, print Not Weird.
> 
> Solution:
> ```python
> #!/bin/python3
> 
> import math
> import os
> import random
> import re
> import sys
> 
> def is_valid_input(num):
>     if (num >= 1 and num <= 100):
>         return True
>     return False
> 
> 
> def solution(num):
>     if(is_valid_input(num)):
>         if (num % 2 != 0):
>             print("Weird")
>         else:
>             if(num >= 6 and num <= 20):
>                 print("Weird")
>             else:
>                 print("Not Weird")
> 
> 
> if __name__ == '__main__':
>     n = int(input().strip())
>     solution(n)
> ```


#### Arithmetic Operators
> Problem -> [URL](https://www.hackerrank.com/challenges/python-arithmetic-operators)
> <br>
> <br>
> Difficulty Level: Easy
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Validate user input, constraints `1 <= a,b <= 10 ^ 10`.
> 3. Print sum, difference and product.
>  
> Solution:
> ```python
> lower_bound = 1
> upper_bound = 10 ** 10
> 
> def is_valid_input(num):
>     if(num >= lower_bound and num <= upper_bound):
>         return True
>     return False
> 
> 
> def solution(num1, num2):
>     if(is_valid_input(num1) and is_valid_input(num2)):
>         print(num1 + num2)
>         print(num1 - num2)
>         print(num1 * num2)
> 
> 
> if __name__ == '__main__':
>     a = int(raw_input())
>     b = int(raw_input())
>     solution(a, b)
> ```


#### Python: Division
> Problem -> [URL](https://www.hackerrank.com/challenges/python-division/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Print the result of integer division in line 1 and result of float division in line 2.
>  
> Solution:
> ```python
> def solution(num1, num2):
>     print(num1 // num2)
>     print(num1 / num2)
> 
> 
> if __name__ == '__main__':
>     a = int(input())
>     b = int(input())
>     solution(a, b)
> ```


#### Loops
> Problem -> [URL](https://www.hackerrank.com/challenges/python-loops/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Validate user input, constraints `1 <= n <= 20`.
> 3. Iterate through each number in range of 0 until n and print square of number.
>  
> Solution:
> ```python
> def is_valid_input(num):
>     if(num >= 1 and num <= 20):
>         return True
>     return False
> 
> 
> def solution(num):
>     if(is_valid_input(num)):
>         for i in range(0, num):
>             print(i ** 2)
> 
> 
> if __name__ == '__main__':
>     n = int(input())
>     solution(n)
> ```


#### Write a function
> Problem -> [URL](https://www.hackerrank.com/challenges/write-a-function/problem)
> <br>
> Difficulty Level: Medium
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Validate user input, constraints `1900 <= year <= 10 ^ 5`.
> 3. If year divisible by 4 and divisible by 100, then year is not leap year.
> 4. If year divisible by 4 and divisible by 400 or only divisible by 4, then year is leap.
> 5. All other cases, year will not be leap.
> 
> Solution:
> ```python
> lower_bound = 1900
> upper_bound = 10 ** 5
> 
> def is_valid_input(n):
>     if(n >= lower_bound and n <= upper_bound):
>         return True
>     return False
> 
> 
> def is_leap(year):
>     if(is_valid_input(year)):
>         if(year % 4 == 0):
>             if (year % 400 == 0):
>                 return True
>             elif (year % 100 == 0):
>                 return False
>             else:
>                 return True
>     return False
> 
> 
> year = int(input())
> print(is_leap(year))
> ```


#### Print Function
> Problem -> [URL](https://www.hackerrank.com/challenges/python-print/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Validate user input, constraints `1 <= n <= 150`.
> 3. For number in range of 1 to n, use print and replace default end character '\n' with empty string.
> 
> Solution:
> ```python
> def is_valid_input(num):
>     if(num >= 1 and num <= 150):
>         return True
>     return False
> 
> 
> def solution(num):
>     if (is_valid_input(num)):
>         for i in range(1, num + 1):
>             print(i, end="")
> 
> 
> if __name__ == '__main__':
>     n = int(input())
>     solution(n)
> ```
