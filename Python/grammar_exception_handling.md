예외 처리
===

## 1. 오류의 종류
1. 프로그램 실행 전에 발생하는 오류 : 구문 오류(syntax error)
2. 프로그램 실행 후에 발생하는 오류 : 런타임 오류(runtime error) or 예외(exception)

## 2. 예외 처리
### 2.1 기본 예외 처리 (조건문)
```python
if 조건:
  예외가 발생할 가능성이 있는 코드
else:
  예외가 발생햇을 때 실행할 코드
```

### 2.2 `try except` 구문
```python
try:
  예외가 발생할 가능성이 있는 코드
except:
  예외가 발생햇을 때 실행할 코드
```
- except 뒤에 `pass` 키워드를 넣어 함께 활용하기도 한다

### 2.3 `try except else` 구문
```python
try:
  예외가 발생할 가능성이 있는 코드
except:
  예외가 발생햇을 때 실행할 코드
else:
  예외가 발생하지 않았을 때 실행할 코드
```

### 2.4 `finally` 구문
```python
try:
  예외가 발생할 가능성이 있는 코드
except:
  예외가 발생햇을 때 실행할 코드
else:
  예외가 발생하지 않았을 때 실행할 코드
finally:
  무조건 실행할 코드
```
- finally 키워드를 사용할 때
\- 함수 내부에 `return` 키워드를 사용할 때
\- 반복문 내부에 `break` 키워드를 사용할 때

### 2.5 구문의 조합
- try구문 뒤에는 반드시 except 구문 또는 finally 구문이 있어야 한다
- else구문은 반드시 except 구문 뒤에서 사용해야 한다
```python
# 경우의 수
try + except
try + except + else
try + except + finally
try + except + else + finally
try + finally
```

## 3. 예외 고급
### 3.1 예외 객체
```python
try:
  예외가 발생할 가능성이 있는 코드
except 예외의 종류 as 예외 객체를 활용할 변수 이름:
  예외가 발생햇을 때 실행할 코드
```

### 3.2 예외 구분 방법
- 예외의 종류가 뭔지 모를 때는, 모든 예외의 어머니 클래스 `Exception`을 사용
```python
try:
  예외가 발생할 가능성이 있는 코드
except Exception as exception:
  print("type(exception):", type(exception))
  print("exception:", exception)
```
- 조건문으로 예외 구분하기
```python
try:
  a=[273, 103, 52, 57, 100]
  number = int(input("정수 입력(0~4까지 입력해주세요> "))
  print(a[number])
except Exception as exception:
  if type(exception) == ValueError:
    print("값에 문제가 있습니다")
  elif type(exception) == IndexError:
    print("0~4까지를 입력해주세요")
```

- except 구문으로 예외 구분하기
```python
try:
  a=[273, 103, 52, 57, 100]
  number = int(input("정수 입력(0~4까지 입력해주세요> "))
  print(a[number])
except ValueError as exception:
  print("값에 문제가 있습니다.")
except IndexError as exception:
  print("0~4까지 입력해주세요")
except Exception as exception:
  print("알 수 없는 예외가 발생했습니다.")
```

### 3.3 예외 강제 발생
- `raise` 예외객체
```python
raise Exception("안녕하세요")
# riase ValueError("Hello")
```
아직 구현되지 않은 부분이어서 그냥 넘어갈 경우   
나중에 큰 문제가 발생하기 때문에 강제 종료를 해야할 때 사용

___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
