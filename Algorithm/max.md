# 최댓값 알고리즘 (Max)
자료구조에서 가장 큰 값을 찾는 알고리즘
___
## 예제 1
```python
class MaxAlgorithm:
  def __init__(self, ns):
    self.nums = ns
    self.maxNum = 0
  
  def getMaxNum(self):
    self.maxNum = self.nums[0]
    
    for n in self.nums:
      if self.maxNum < n:
        self.maxNum = n
        
    return self.maxNum;
    
max = MaxAlgorithm([4, 6, -7, 13, -24, 8])
maxNum = max.getMaxNum()
print(f'maxNum: {maxNum}')
```
