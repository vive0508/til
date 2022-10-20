집합 자료형
===


## 1. 집합 자료형의 특징
- 집합은 중복을 허용하지 않는다
- 집합은 순서가 없다

## 2. 집합의 형변환
집합을 리스트로 만드는 방법
```python
list_set = set(리스트명)
```
리스트를 집합으로 만드는 방법
```python
list(집합명)
```

## 3. 집합 관련 함수
- set()
```python
sample = set([1, 1, 1, 2, 3, 3, 3, 3, 3])
print(sample)
```
{1, 2, 3}

- 세트명.add()
```python
setA = set()

setA.add(1)
setA.add(1)
setA.add(1)
setA.add(1)
setA.add(2)
setA.add(2)
setA.add(2)
setA.add(3)

print(setA)
```
{1, 2, 3}

- 세트명.update()
```python
# 여러개의 값을 한 번에 업데이트
# 리스트, 튜플, 집합을 모두 한 번에 업데이트 할 수 있다
setA = set()

setA.update([1, 1, 2, 2, 3, 3])
print(setA)
```
{1, 2, 3}

- 세트명.remove()
```
setA = set()

setA.update([1, 1, 2, 2, 3, 3])
setA.remove(3)

print(setA)
```
{1, 2}

## 4. 집합자료형의 연산
### 3.1 합집합
- set1.union(set2)
- set1 | set2
   
### 3.2 교집합
- set1.intersection(set2)
- set1 & set2   
   
### 3.3 차집합
- set1.dfference(set2)
- set1-set2

   
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
* [이것이 취업을 위한 코딩 테스트다 with 파이썬(나동빈)](https://www.hanbit.co.kr/store/books/look.php?p_code=B8945183661)
