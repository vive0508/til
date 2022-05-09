# 버블 정렬(bubble sort)
- 두 인접한 원소를 검사하여 정렬하는 방법이다.
- 인덱스의 값을 순차적으로 비교하면서 큰 숫자를 가장 끝으로 옮긴다.
- 상당히 느리지만, 코드가 단순하기 때문에 자주 사용된다.

[개념 설명(위키백과)](https://ko.wikipedia.org/wiki/%EA%B1%B0%ED%92%88_%EC%A0%95%EB%A0%AC)

___
### 예제 1
```python
nums = [14, 8, 5, 21, 0]
print(f'unsorted nums : {nums}')

length = len(nums)-1

for i in range(length):
    for j in range(length-i):
        if nums[j] > nums[j+1]:
            nums[j], nums[j+1] = nums[j+1], nums[j]
        print(nums)
    print()

print(f'sorted nums : {nums}')
```
unsorted nums : [14, 8, 5, 21, 0]   
[8, 14, 5, 21, 0]   
[8, 5, 14, 21, 0]   
[8, 5, 14, 21, 0]   
[8, 5, 14, 0, 21]   
   
[5, 8, 14, 0, 21]   
[5, 8, 14, 0, 21]   
[5, 8, 0, 14, 21]   
   
[5, 8, 0, 14, 21]   
[5, 0, 8, 14, 21]   
   
[0, 5, 8, 14, 21]   
   
sorted nums : [0, 5, 8, 14, 21]   

### 예제 2
- 모듈
```python
import copy

def bubbleSort(array, deepCopy=True):

  if deepCopy:
      cArray= copy.copy(array)
  else:
      cArray=array

  length = len(cArray)-1
  
  for i in range(length):
    for j in range(length-i):
        if cArray[j] > cArray[j+1]:
            cArray[j], cArray[j+1] = cArray[j+1], cArray[j]
            
  return cArray
```
- 실행 파일 (feat. 깊은 복사)
```python
import random as rd
import module as st

players = []

for i in range(20):
    players.append(rd.randint(175, 190))

sortedPlayers = st.bubbleSort(players)

print(f'unsorted players : {players}')
print(f'sorted players : {sortedPlayers}')
```
