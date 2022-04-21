클래스
===

## 1. 객체(Object)
- 어떠한 속성과 행위를 가지고 있는 모든 것

### 1.1 객체 지향 프로그래밍(Object Oriented Programming Language)
- 파이썬은 객체를 기반으로 프로그램을 만드는 프로그래밍 언어이다   
- 파이썬의 모든 코드들을 Class 기반으로 만들겠다   
- 모든 데이터 타입은 클래스이다 (ex. str data type -> str class)   

```
# str class를 기반으로 만들어진 객체 변수
p = 'python' 

# str 클래스의 메서드/변수 리스트업
dir(p)

# 두 개의 결과가 같음
p.__add__(' is easy')
p + ' is easy'
```

### 1.2 객체지향 프로그래밍의 4가지 특징 : 추상화, 캡슐화, 상속, 다형성   
pass

___

## 2. 클래스
### 2.1 클래스 선언
- 클래스 : 객체를 쉽고 편리하게 생성하기 위해 만들어진 구문
```python
# 클래스(틀) 선언 : 학생은 이름이라는 속성을 갖고 있다
class 클래스이름:
  클래스 내용

# 객체(실체화) 생성 : 학생 이름은 김재현이다
클래스이름()
```
- 클래스 == 붕어빵틀 == 설계도
- 붕어빵 == (인스턴스) (객체) 변수 == instance object variable

### 2.2 식별자
| 식별자 | 표기법 |
|:--:|:--:|
|스네이크 케이스|snake_case|
|캐멀 케이스|camelCase|
|파스칼 케이스|PascalCase|
|케밥 케이스|kebab-case|   

클래스는 파스칼 케이스(Pascal Case)를 사용한다   


### 2.3 생성자
- 인스턴스 : 클래스를 기반으로 생성한 객체를 의미한다
- 생성자 : 클래스 이름과 같은 신스턴스를 생성할 때 사용하는 함수이다
```python
# 클래스 내부의 함수들은 첫번째 매개변수로 self를 가진다   
class Student:
  # 생성자
  def __init__(self):
    print("객체가 생성되었습니다.")
  # 소멸자(잘 사용되지는 않음)
  def __del__(self):
    print("객체가 소멸되었습니다.")
    
# 인스턴스(객체) 생성
student = Student()
```
self는 키워드가 아니라 단순한 식별자이기 때문에, 변수 이름을 활용해도 가능은 하다   
하지만 개발자들의 약속으로 self를 사용하는 것이 일반적이다  

### 2.4 클래스의 속성 선언하기
- 내부에 속성을 생성 혹은 접근할 때는 `self.속성`를 사용한다
```python
class Student:
  def __init__(self, 이름, 생년월일):
    print("객체가 생성되었습니다.")
    self.이름 = 이름
    self.생년월일 = 생년월일
    
student = Student("김재현", 960508)
print(student.이름, student.생년월일)
```
객체가 생성되었습니다   
김재현 960508

### 2.5 클래스의 함수 선언하기
- 내부에 함수을 생성 혹은 접근할 때는 `self.행위`를 사용한다
```python
# 클래스가 가진 함수를 메소드(method)라고 부르기도 한다
class Student:
  def __init__(self, 이름, 생년월일):
    print("객체가 생성되었습니다.")
    self.이름 = 이름
    self.생년월일 = 생년월일
  def 출력(self):
    print(self.이름, self.나이)
    
student = Student("김재현", 960508)
student 출력()
```
객체가 생성되었습니다   
김재현 960508


### 2.6 특수한 이름의 함수("__")

```python
class Student:
  def __str__(self)
    return "{}{}".format(self.이름, self.생년월일)
  def __init__(self, 이름, 생년월일):
    print("객체가 생성되었습니다.")
    self.이름 = 이름
    self.생년월일 = 생년월일
     
student = Student("김재현", 960508)
print(str(student))
```
김재현 960508

### 2.7 비교 연산자의 영어표현
| 이름 | 영어 | 설명 |
| :--: | :-- | :-- |
| eq | equal | 같다 |
| ne | not equal | 다르다 |
| gt | greater than | 크다 |
| ge | greater than or equal | 크거나 같다 |
| lt | less than | 작다 |
| le | less than or equal | 작거나 같다 |
___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
