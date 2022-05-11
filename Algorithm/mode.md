# 최빈값 알고리즘 (Mode)
자료구조에서 빈도수가 가장 많은 값을 찾는 알고리즘
___
## 예제 1

- 최댓값 알고리즘을 활용하여 클래스 생성
```python
class MaxAlgorithm:
    def __init__(self, ns):
        self.nums = ns
        self.maxNum = 0
        self.maxNumIdx = 0
  
    def setMaxIdxAndNum(self):
        self.maxNum = self.nums[0]
        self.maxNumIdx = 0
    
        for i, n in enumerate(self.nums):
          if self.maxNum < n:
            self.maxNum = n
            self.maxNumIdx = i
      
    def getMaxNum(self):
        return self.maxNum

    def getMaxNumIdx(self):
        return self.maxNumIdx
```

- 자료구조의 최댓값 출력
```python
nums = [1, 3, 7, 6, 7, 7, 7, 12, 12, 17]

max = MaxAlgorithm(nums)
max.setMaxIdxAndNum()

maxNum = max.getMaxNum()
maxNumIdx = max.getMaxNumIdx()

print(f'maxNum : {maxNum}')
print(f'maxNumIdx : {maxNumIdx}')
```

- 최댓값을 활용하여 최빈값 추출
```python
index = [0 for i in range(maxNum + 1)]

for n in nums:
    index[n] += 1

print(f'index : {index}')

mode = MaxAlgorithm(index)
mode.setMaxIdxAndNum()

maxNum = mode.getMaxNum()
maxNumidx = mode.getMaxNumIdx()

print(f'maxNum : {maxNum}')
print(f'maxNumIdx : {maxNumidx}')
print(f'{maxNumidx}의 빈도수가 "{maxNum}회"로 가장 높다')
```
