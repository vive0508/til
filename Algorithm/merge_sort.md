# 병합 정렬(Merge Sort)
자료구조를 분할하고 각각의 분할된 자료구조를 정렬한 후 다시 병합하여 정렬한다.

## 예제 1
```python
def mSort(ns):
    
    if len(ns) < 2:
        return ns
    
    midIdx = len(ns)//2
    leftNums = mSort(ns[0:midIdx])
    rightNums = mSort(ns[midIdx:len(ns)])
    
    mergeNums = []
    leftIdx = 0; rightIdx = 0
    
    while leftIdx < len(leftNums) and rightIdx < len(rightNums):
        if leftNums(leftIdx) < rightNums[rightIdx]:
            mergeNums.append(leftNums[leftIdx])
            leftIdx += 1

        else:
            mergeNums.append(rightNums[rightIdx])
            rightIdx += 1
    
    mergeNums = mergeNums + leftNums[leftIdx:]
    mergeNums = mergeNums + rightNums[rightIdx:]
    
    return mergeNums

nums = [8, 1, 4, 3, 2, 5, 10, 6]
a = mSort(nums)     
```
오류 해결 필요
