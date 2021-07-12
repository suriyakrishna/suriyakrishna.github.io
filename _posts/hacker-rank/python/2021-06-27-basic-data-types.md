---
layout: post
title: Hacker Rank - Python Basic Data Types
date: 2021-06-27 16:37:00 +0530
categories: hackerrank python
---

[Hacker Rank Python Challenges](https://www.hackerrank.com/domains/python)

***Python Version 3***

#### Problems
1. [List Comprehensions](#list-comprehensions)
1. [Find the Runner-Up Score!](#find-the-runner-up-score)
1. [Nested Lists](#nested-lists)
1. [Finding the percentage](#finding-the-percentage)
1. [Lists](#lists)
1. [Tuples](#tuples)


#### List Comprehensions
> Problem -> [URL](https://www.hackerrank.com/challenges/list-comprehensions/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user. 
> 2. Create a empty list.
> 3. For each combination on x, y and z check sum not equal to n. If true, append the pair to the list.
> 4. Finally print the list
>  
> Solution:
> ```python
> def solution(x, y, z, n):
>     result = []
>     for i in range(0, x + 1):
>         for j in range(0, y + 1):
>             for k in range(0, z + 1):
>                 if (i + j + k != n):
>                     result.append([i, j, k])
>     print(result)
> 
> 
> if __name__ == '__main__':
>     x = int(input())
>     y = int(input())
>     z = int(input())
>     n = int(input())
>     solution(x,y,z,n)
> ```


#### Find the Runner-Up Score!
> Problem -> [URL](https://www.hackerrank.com/challenges/find-second-maximum-number-in-a-list/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Validate user input, constraints `2 <= n <= 10` and `-100 <= score[i] <= 100`.
> 3. define two variable first_max and second_max with any minimum value less than -100.
> 4. Iterate through score, 
>    for each score check,
> - if score is greater that first_max then we need to update second_max = first_max and update first_max = score.
> - else if score is greater than second_max and less than first_max then we need to update second_max with score.
> - else do nothing
> 5. Finally, return second_max  
>  
> Solution:
> ```python
> def is_valid_input(n, scores):
>     if(n != len(scores)):
>         return False
>     if(n >= 2 and n <= 10):
>         for score in scores:
>             if(score < -100 or score > 100):
>                 return False
>         return True
>     return False
>     
> 
> def solution(n, scores):
>     if(is_valid_input(n, scores)):
>         first_max = -101
>         second_max = -101
>         for score in scores:
>             if (score > first_max):
>                 first_max, second_max = score, first_max
>             elif(score > second_max and score < first_max):
>                 second_max = score
>         print(second_max)
> 
> 
> if __name__ == '__main__':
>     n = int(input())
>     arr = list(map(int, input().split()))
>     solution(n, arr)
> ```


#### Nested Lists
> Problem -> [URL](https://www.hackerrank.com/challenges/nested-list/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user. 
> 2. Validate user input, constraints `2 <= N <= 5`.
> 3. Crete a empty dict.
> 4. define two variable first_min and second_min with any maximum value, here I used 10 ^ 5.
> 5. Iterate through student records, for each record,
> > - Considering score as key, store student names as list for each scores in the dict
> > - Find the second minimum score,
> >     -  If score < first_min, then assign first_min = score and second_min = first_min
> >     -  else if score > first_min and score < second_min, then assign second_min = score
>  6. Finally, get the names from dict for the second_min score from the dict.
>  7. Sort the name and print as string with next line character for each name.
>  
> Solution:
> ```python
> def is_valid_input(records):
>     num_records = len(records)
>     if(num_records >= 2 and num_records <= 5):
>         return True
>     return False
> 
> 
> def solution(records):
>     if(is_valid_input(records)):
>         names = {}
>         first_min = 10 ** 5
>         second_min = 10 ** 5
>         for record in records:
>             # Create dict of scores with all names associated to scores.
>             score = record[1]
>             name = record[0]
>             if score in names:
>                 names[score].append(name)
>             else:
>                 names[score] = [name]
>             # Find Second Min Score
>             if score < first_min:
>                 first_min, second_min = score, first_min
>             elif score > first_min and score < second_min:
>                 second_min = score
>         print("\n".join(sorted(names[second_min])))
> 
> 
> if __name__ == '__main__':
>     records = []
>     for _ in range(int(input())):
>         name = input()
>         score = float(input())
>         records.append([name, score])
>     solution(records)
> ```


#### Finding the percentage
> Problem -> [URL](https://www.hackerrank.com/challenges/finding-the-percentage/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Validate user input, constraints `2 <= n <= 10`, `0 <= marks[i] <= 100` and `len(marks) == 3`.
> 3. Calculate average mark for given student name.
> 4. Print the average with 2digit precision.
> 
> Solution:
> ```python
> def is_valid_input(students):
>     records_length = len(students)
>     if (records_length >= 2 and records_length <= 10):
>         for k,v in students.items():
>             if(len(v) != 3):
>                 return False
>             if(not(all(map(lambda x: x >= 0 and x <= 100, v)))):
>                 return False
>         return True
>     return False
> 
> 
> def solution(students, name):
>     if(is_valid_input(students)):
>         average = sum(students[name])/len(students[name])
>         print("{:.2f}".format(float(average)))
> 
> 
> if __name__ == '__main__':
>     n = int(input())
>     student_marks = {}
>     for _ in range(n):
>         name, *line = input().split()
>         scores = list(map(float, line))
>         student_marks[name] = scores
>     query_name = input()
>     solution(student_marks, query_name) 
> ```



#### Lists
> Problem -> [URL](https://www.hackerrank.com/challenges/python-lists/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Create an empty list.
> 3. For each user input, Based on type of list operation, call builtin list operations with required parameters and we need to cast the string input to int before storing it in the list.
> 
> Solution:
> ```python
> def solution(n):
>     nums = []
>     for i in range(0, n):
>         user_input = str(input()).split(" ")
>         operation = user_input[0]
>         if(operation.lower() == "insert"):
>             index = int(user_input[1])
>             value = int(user_input[2])
>             nums.insert(index, value)
>         elif(operation.lower() == "print"):
>             print(nums)
>         elif(operation.lower() == "remove"):
>             value = int(user_input[1])
>             nums.remove(value)
>         elif(operation.lower() == "append"):
>             value = int(user_input[1])
>             nums.append(value)
>         elif(operation.lower() == "sort"):
>             nums = sorted(nums)
>         elif(operation.lower() == "pop"):
>             nums.pop()
>         elif(operation.lower() == "reverse"):
>             nums.reverse()
> 
> 
> if __name__ == '__main__':
>     N = int(input())
>     solution(N)
> ```


#### Tuples
> Problem -> [URL](https://www.hackerrank.com/challenges/python-tuples/problem)
> <br>
> Difficulty Level: Easy
> <br>
> <br>
> Pseudocode:
> 1. Read input from user.
> 2. Convert list to tuple.
> 3. Print the hash string for tuple using inbuilt function `hash()`.
> 
> Solution:
> ```python
> def solution(nums):
>     print(hash(tuple(nums)))
> 
> 
> if __name__ == '__main__':
>     n = int(input())
>     integer_list = map(int, input().split())
>     solution(integer_list) 
> ```