# 최솟값 알고리즘 (Min)
자료구조에서 가장 작은 값을 찾는 알고리즘
___
## 예제 1
```python
class MinAlgorithm:
  def __init__(self, ns):
    self.nums = ns
    self.minNum = 0
  
  def getMinNum(self):
    self.minNum = self.nums[0]
    
    for n in self.nums:
      if self.minNum > n:
        self.minNum = n
        
    return self.minNum;


min = MinAlgorithm([4, 6, -7, 13, -24, 8])
minNum = min.getMinNum()
print(f'minNum: {minNum}')
```
