# 삽입 정렬(insertion sort)
- 자료 배열의 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입함으로써 정렬하는 알고리즘이다.
- k번째 반복 후의 결과 배열은, 앞쪽 k + 1 항목이 정렬된 상태이다.
- 배열이 길어질수록 효율이 떨어진다. 다만, 구현이 간단하다는 장점이 있다.
- 선택 정렬이나 거품 정렬 알고리즘에 비교하여 빠르다.

[개념 설명(위키백과)](https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC)
___
## 예제 1

```python
# ascending
nums = [7, 11, 3, 1, 2]

for i1 in range(1, len(nums)):
    i2 =  i1 - 1
    cNum = nums[i1]
    
    while nums[i2] > cNum and i2 >=0:
        nums[i2+1] = nums[i2]
        i2 -= 1
        
    nums[i2 +1] = cNum
    print(f'nums: {nums}')
    

#descending

nums = [2, 7, 3, 11, 1]

for i1 in range(1, len(nums)):
    i2 =  i1 - 1
    cNum = nums[i1]
    
    while nums[i2] < cNum and i2 >=0:
        nums[i2+1] = nums[i2]
        i2 -= 1
        
    nums[i2 +1] = cNum
    print(f'nums: {nums}')
```
<!--
## 예제 2
- 모듈
```python
class SortNumbers:
    def __init__(self, ns, asc=True):
        self.nums= ns
        self.isAsc = asc

    def isAscending(self, flag):
        self.isAsc = flag

    def setSort(self):
        for i1 in range(1, len(self.nums)):
            i2 = i1 -1
            cNum = self.nums[i1]

            if self.isAsc:
                while self.nums[i2] > cNum and i2 >= 0:
                    self.nums[i2 +1] = self.nums[i2]
                    i2 -= 1
            
            else:
                while self.num[i2] < cNum and i2 >= 0:
                    self.nums[i2 +1] = self.nums[i2]
                    i2 -= 1

            self.nums[i2 + 1] = cNum

def getSortedNumbers(self):
    return self.nums

def getMinNumber(self):
    if self.isAsc:
        return self.nums[0]
    else:
        return self.nums[len(self.nums)-1]

def getMaxNum(self):
    if self.isAsc:
        return self.nums[len(self.nums)-1]
    else:
        return self.nums[0]
```

- 실행파일
```python
import random
import module as sn

nums = random.sample(range(1,1000), 100)

print(f'not sorted numbers: {nums}')

sn = sn.SortNumbers(nums)

# ascending
sn.setSort()
sortedNumbers = sn.getSortedNumbers()
print(f'sortedNumbers by ASC: {sortedNumbers}')

# descending
sn.isAscending(False)
sn.setSort()
sortedNumbers = sn.getSortedNumbers()
print(f'sortedNumbers by DESC : {sortedNumbers}')

# min & max
print(f'min : {sn.getMinNumber()}')
print(f'max : {sn.getMaxNumber()}')
```
-->
