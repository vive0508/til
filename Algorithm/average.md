# 평균 알고리즘 (Average)
## 예제 1
- 평균을 구하는 일반적인 방법
```python
import random

nums = random.sample(range(0, 100), 10)
print(f'nums: {nums}')

total = 0
for n in nums:
  total += n
  
average = total / len(nums)
print(f'average : {round(average, 2)}')
```

## 예제 2
- 조건과 함께 평균을 구하는 방법
```python
# 50이상 90이하 수들의 평균
import random

nums = random.sample(range(0, 100), 30)
print(f'nums: {nums}')

total = 0
targetNums = []

for n in nums:
  if n >= 50 and n <=90:
    total += n
    targetNums.append(n)
  
average = total / len(targetNums)
print(f'targetNums : {targetNums}')
print(f'average : {round(average, 2)}')
```

## 예제 3
- 조건과 함께 평균을 구하는 방법
```python
# 정수들의 평균
nums = [4, 5.12, 0, 5, 7.34, 9.1, 9, 3, 3.159, 1, 11, 12.789]
print(f'nums: {nums}')

total = 0
targetNums = []

for n in nums:
  if n-int(n)==0:
    total += n
    targetNums.append(n)
  
average = total / len(targetNums)
print(f'targetNums : {targetNums}')
print(f'average : {round(average, 2)}')
```
