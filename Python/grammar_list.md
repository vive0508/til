리스트 자료형
===

대괄호 안에 요소를 쉼표로 구분하여 입력한다.   
리스트 대신에 배열 혹은 테이블이라고 부르기도 한다. 
   
## 1. 리스트 관련 함수

### 1.1 리스트 생성
- 빈 리스트를 생성하는 두가지 방법
```python
list_a = []
list_b = list()
```
- range 함수를 활용해 리스트를 초기화할 수 있다.
```
list_c = list(range(3))
print(list_c)
```
[0, 1, 2]

- 내부의 요소를 반복문을 통해 넣을 수도 있다.
```python
sample= [0 for _ in range(5)]
print(sample)
```
[0, 0, 0, 0, 0]

### 1.2 연결, 반복, 요소길이
```python
# 리스트 샘플
list_a = [1, 2, 3]
list_b = [4, 5, 6]
```
- list_a + list_b = [1, 2, 3, 4, 5, 6]
- list_a * 3 = [1, 2, 3, 1, 2, 3]
- len(list_a) = 3

### 1.4 리스트 추가
- 리스트명.append(요소)
- 리스트명.insert(위치, 요소)   
- 리스트_a.extend(리스트_b)

### 1.5 리스트 요소 제거
- del 리스트명[인덱스]
- 리스트명.pop(인덱스)
- 리스트명.remove(값)
- 리스트명.clear()

### 1.6 리스트 슬라이싱
- 리스트명[:]
- 리스트명[slice()]

### 1.7 리스트 요소 갯수, 위치
- 리스트명.count(값)
- 리스트명.index()

### 1.8 리스트 내부 리스트 조회
```
players = [ ['수비', '김민재'], ['미드필더', '황인범'], ['공격수', '황희찬'] ]

for position, player in players:
   print('{} 포지션 : {}'.format(position, player))
```

수비 포지션 : 김민재   
미드필더 포지션 : 황인범   
공격수 포지션 : 황희찬


___
## 2. 리스트 관련 함수
### 2.1 리스트 정렬
- 오름차순 정렬 : 리스트명.sort()
- 내림차순 정렬 : 리스트명.sort(reverse=True)

### 2.2 셔플(shuffle)
```python
import random as r

sample = list(range(10+1))
print(sample)

r.shuffle(sample)
print(sample)
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]    
[7, 1, 2, 0, 6, 9, 3, 10, 5, 4, 8]   

### 2.3 리스트 요소 인덱스 번호 확인(`enumerate()`)
```
array = ['a', 'b', 'c']

for i, value in enumerate(array)
  print("{}번째 요소는 {}입니다.".format(i, value))
```
0번째 요소는 a입니다.
1번째 요소는 b입니다.
2번째 요소는 c입니다.

### 2.4 리스트 요소 뒤집기(`reversed()`)
```python
list = [1, 2, 3, 4, 5]
list_reversed = reversed(list)
print(list_reversed)
```
[5, 4, 3, 2, 1]

### 2.5 최소,최대,합
| 함수 | 기능 |
| -- | -- |
| min() | 리스트 내부에서 최솟값을 찾는다 |
| max() | 리스트 내부에서 최댓값을 찾는다 |
| sum() | 리스트 내부의 값을 모두 더한다 |

___

## 3. 리스트 내포(List comprehension)
### 3.1 리스트 내포 예시
**리스트 이름 = [ 표현식 for 반복자 in 반복할 수 있는 것 if 조건문]**

```python
array = []
for i in range(0, 20, 2):
  array.append(i*i)
```

위의 코드 세줄을 한 줄로 표현 할 수 잇음
```python
array = [i*i for i in range(0, 20, 2)]
```

### 3.2 2차원 리스트 초기화
```python
n = 4
m = 3
array = [[0]*m for _ in range(n)]
print(array)
```
[[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]

## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
