조건문
===
- 조건문은 프로그램의 흐름을 제어하는 문법이다
- 조건문을 이용해 조건에 다라 프로그램 로직을 설정할 수 있다
- 파이썬에서는 코드 블록을 들여쓰기(Indent)로 지정한다
- 파이썬 스타일 가이드라인에서는 4개의 공백 문자를 표준으로 설정하고 있다

## 0. 조건문
```python
# A if 조건식 else B
조건식의 결과가 True이면 A실행, 그렇지 않으면 B실행
```
## 1. if~else 구문
```python
if 조건 :
    조건이 참일 때 실행할 문장 ** 들여쓰기 주의
else:
    조건이 거짓일때 실행할 문장
```
## 2. elif 구문
```python
if 조건 A:
    조건 A가 참일 때 실행할 문장
elif 조건 B:
    조건 B가 참일 때 실행할 문장
elif 조건 C:
    조건 C가 참일 때 실행할 문장
```
## 3. pass
- 프로그래밍 전체 골격을 잡아 놓을 때 사용한다   
- 조건이 참 혹은 거짓일 때 실행할 문장이 미구현 상태일 때 pass 입력한다   

## 4. 기타
- 조건문에서 실행될 소스코드가 한 줄인 경우. 굳이 줄 바꿈을 하지 안혹도 간략하게 표현할 수 있다.
```python
score = 85

if score >=80: result = "Success"
else : result = "Fail"
```
- 조건부 표현식(Conditional Expression)은 if~else문을 한 줄에 작성할 수 있도록 해준다.
```python
score = 85
result = "Success" if socre>=80 else "Fail"
print(result)
```


## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
* [이것이 취업을 위한 코딩 테스트다 with 파이썬(나동빈)](https://www.hanbit.co.kr/store/books/look.php?p_code=B8945183661)
