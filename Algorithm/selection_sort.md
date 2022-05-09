# 선택 정렬 알고리즘 (selection sort)
제자리 정렬 알고리즘의 하나로, 다음과 같은 순서로 이루어진다.
1. 주어진 리스트 중에 최소값을 찾는다.
2. 그 값을 맨 앞에 위치한 값과 교체한다.
3. 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다.

[개념설명(위키백과)](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)

___
## 예제 1
```python
nums = [4, 2, 5, 1, 3]

print(f'nums: {nums}')

for i in range(len(nums) -1):
  minIdx = i

  for j in range(i+1, len(nums)):
    if nums[minIdx] > nums[j]:
      minIdx = j
      
  #tempNum = nums[i]
  #nums[i] = nums[minIdx]
  #nums[minIdx] = tempNum
  nums[i], nums[minIdx] = nums[minIdx], nums[i]
  print(f'nums: {nums}')

print(f'final nums: {nums}')
```

## 예제 2
- 모듈
```python
def sortNumber(ns, asc=True):

    if asc:
        for i in range(len(ns)-1):
            minIdx=1

            for j in range(i+1, len(ns)):
                if ns[minIdx] > ns[j]:
                    minIdx = j

            ns[i], ns[minIdx] = ns[minIdx], ns[i]
    else:
        for i in range(len(ns)-1):
            minIdx=1

            for j in range(i+1, len(ns)):
                if ns[minIdx] < ns[j]:
                    minIdx = j

            ns[i], ns[minIdx] = ns[minIdx], ns[i]

    return ns 
```

- 실행파일
```python
import random
import module as sn
import copy

scores = random.sample(range(50, 101), 20)

print(f'scores : {scores}')
result = sn.sortNumber(copy.deepcopy(scores))
print(f'result: {result}')

print(f'scores : {scores}')
result = sn.sortNumber(scores, asc=False)
print(f'result: {result}')
```
