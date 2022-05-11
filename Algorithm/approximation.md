# 근삿값 알고리즘 (Approximation)

자료구조 중 입력한 값과 가장 가까운 값을 구하는 알고리즘
___
## 예제 1

```python
import random

nums = random.sample(range(0,50),20)
print(f'nums: {nums}')

inputNum = int(input('input number: '))
print(f'inputNum: {inputNum}')

nearNum = 0
minNum = 50

for n in nums:
    absNum = abs(n-inputNum)
    
    if absNum < minNum:
        minNum = absNum
        nearNum = n

print(f'nearNum: {nearNum}')
```
