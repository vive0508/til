리스트 자료형
===

대괄호 안에 요소를 쉼표로 구분하여 입력한다.   
리스트 대신에 배열 혹은 테이블이라고 부르기도 한다. 
   
## 1. 리스트 관련 함수
### 1.1 연결, 반복, 요소길이
```python
# 리스트 샘플
list_a = [1, 2, 3]
list_b = [4, 5, 6]
```
- list_a + list_b = [1, 2, 3, 4, 5, 6]
- list_a * 3 = [1, 2, 3, 1, 2, 3]
- len(list_a) = 3

### 1.2 리스트 추가
- 리스트명.append(요소)
- 리스트명.insert(위치, 요소)
- 리스트_a.extend(리스트_b)

### 1.3 리스트 요소 제거
- del 리스트명[인덱스]
- 리스트명.pop(인덱스)
- 리스트명.remove(값)
- 리스트명.clear()

### 1.4 특정 값의 요소 갯수 세기
- 리스트명.count(값)

### 1.4 리스트 정렬
- 오름차순 정렬 : 리스트명.sort()
- 내림차순 정렬 : 리스트명.sort(reverse=True)

### 1.5 리스트 요소 뒤집기(`reversed()`)
```python
list = [1, 2, 3, 4, 5]
list_reversed = reversed(list)
print(list_reversed)
```
[5, 4, 3, 2, 1]


### 1.6 숫자 리스트 관련 함수
| 함수 | 기능 |
| -- | -- |
| min() | 리스트 내부에서 최솟값을 찾는다 |
| max() | 리스트 내부에서 최댓값을 찾는다 |
| sum() | 리스트 내부의 값을 모두 더한다 |

### 1.7 리스트 요소 인덱스 번호 확인(`enumerate()`)
```
array = ['a', 'b', 'c']

for i, value in enumerate(array)
  print("{}번째 요소는 {}입니다.".format(i, value))
```
0번째 요소는 a입니다.
1번째 요소는 b입니다.
2번째 요소는 c입니다.


## 2. 리스트 내포(List comprehension)
### 2.1 리스트 내포 예시
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

### 2.2 2차원 리스트 초기화
```python
n = 4
m = 3
array = [[0]*m for_in range(n)]
print(array)
```
Python에서 반복을 수행하되 반복을 위한   
변수의 값을 무시하고자 할 때, 언더바(_)를 사용한다
