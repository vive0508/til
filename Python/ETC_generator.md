제너레이터
===

## 1. 제너레이터
이터레이터를 직접 만들 때 사용하는 구문   
함수 내부에 yield 라는 키워드가 포함되면 해당 함수는 제너레이터가 된다

### 1.1 `next()`  
```python
def 함수():
  print("출력A")
  print("출력B")
  yeild
  
제너레이터 = 함수()
next(제너레이터)
```
출력A   
출력B   

### 1.2 `yield` 키워드로 값 전달
```python
def 함수():
  print("출력A")
  print("출력B")
  yeild 100
  
제너레이터 = 함수()
값 = next(제너레이터)
print(값)
```
출력A   
출력B   
100   

### 1.3 `yield` 키워드로 양보하기
```python
def 함수():
  print("출력A")
  yeild 100
  print("출력B")
  yeild 200
  print("출력C")
  yeild 300
  print("출력D")
  yeild 400
  
제너레이터 = 함수()
next(제너레이터)
next(제너레이터)
next(제너레이터)
next(제너레이터)
```
출력A   
출력B   
출력C   
출력D   

### 1.4 for 반복문과 함께 사용하기
```python
def 함수():
  print("출력A")
  yeild 100
  print("출력B")
  yeild 200
  print("출력C")
  yeild 300
  print("출력D")
  yeild 400
  
제너레이터 = 함수()
for i in 제너레이터
  pass
  
for i in 제너레이터
  print(i)
```
출력A   
100   
출력B   
200
출력C   
300   
출력D   
400   

### 1.5 reversed (참고)
- 아래 함수를 사용하는 동안 제너레이터만 만들어질 뿐
- 어떠한 데이터도 추가적으로 만들어지지 않는다
- 메모리를 절약할 수 있다
```python
def 반전(리스트):
  for i in range(len(리스트)):
    yield 리스트[-i-1]

제너레이터 = 반전([1, 2, 3, 4, 5])
for i in 제너레이터:
  print(i)
```
5   
4   
3   
2   
1   


___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)


