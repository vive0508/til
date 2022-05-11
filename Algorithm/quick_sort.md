# 퀵 정렬(Quick Sort)
기준 값보다 작은 값과 큰 값으로 분리한 후 다시 합친다.

## 예제 1
```python
def qSort(ns):
    if len(ns) < 2:
        return ns
    
    midIdx = len(ns) // 2
    midVal = ns[midIdx]
    
    smallNums = []
    sameNums = []
    bigNums = []
    
    for n in ns:
        if n < midVal:
            smallNums.append(n)
        elif n == midVal:
            sameNums.append(n)
        else :
            bigNums.append(n)
    
    return qSort(smallNums) + sameNums + qSort(bigNums)

nums = [8, 1, 4, 3, 2, 5, 4, 10, 6, 8]
print(f'qSort(nums) : {qSort(nums)}')
```
