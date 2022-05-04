클래스
===

## 1. 객체(Object)
- 어떠한 속성과 행위를 가지고 있는 모든 것

### 1.1 객체 지향 프로그래밍(Object Oriented Programming Language)
- 객체를 이용한 프로그램으로 객체는 속성과 기능으로 구성된다
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
- 클래스 : 객체를 쉽고 편리하게 생성하기 위해 만들어진 구문 (객체는 클래스로부터 생성된다)
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
- 생성자 : 클래스 이름과 동일한 인스턴스를 생성할 때 사용하는 함수이다

```python
# 클래스 내부의 함수들은 첫번째 매개변수로 self를 가진다   
# 객체가 생성될 때 생성자를 호출하면 __init__()이 자동 호출된다

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
- 객체를 생성할 때 필요한 매개변수는 객체의 속성을 초기화한다. 그리고 이를 레퍼런스 변수에 할당한다
```python
# __init__()에 매개변수를 넣어 속성을 초기화할 수 있다
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

- 객체 속성 변경허기
```python
student.이름 = "홍길동"
print(student.이름, student.생년월일)
```
홍길동, 960508   

### 2.5 클래스의 함수 선언하기
- 내부에 함수을 생성 혹은 접근할 때는 `self.행위`를 사용한다
- 레퍼런스 변수를 통해 객체의 기능에 접근할 수 있다
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

### 2.6 객체 복사 (얕은 복사 / 깊은 복사)
- 레퍼런스 변수는 객체의 메모리 주소를 저장하고 이를 이용해서 객체를 참조한다.
- 얕은 복사 : 객체 주소를 복사하는 것으로 객체 자체가 복사되지 않는다.
- 깊은 복사 : 객체 자체를 복사하는 것으로, 또 하나의 객체가 생성된다.

```python
class Robot:
  def __init__(self, color, height, weight):
    self.color = color
    self.height = height
    self.weight = weight
    
    def printRobotInfo(self):
    print(f'color: {self.color}')
    print(f'height: {self.height}')
    print(f'weight: {self.weight}')

# rb3은 rb1과 동일한 메모리 주소를 공유하게 됨 (얕은 복사)
rb1 = Robot('orange', 100, 50)
rb2 = Robot('red', 200, 70)
rb3 = rb1

## 그래서, rb1의 속성값이 변경되면 rb3도 영향을 받음 (반대로도 마찬가지)
# rb1.color = 'blue'
# rb1.height = 300
# rb1.weight = 100

# 이를 피하기 위해서 사용하는 방법이 깊은 복사
import copy
rb3 = copy.copy(rb1)
```

- 깊은 복사 (feat. 리스트)
```python
scrores = [9, 8, 5, 7, 6, 10] 
scoresCopy = []

scoresCopy = scores

# 첫번째 방법, for문
for s in scores:
  scoresCopy.append(s)

print(f'id(scores): {id(scores)}')
print(f'id(scoresCopy): {id(scoresCopy)}')

# 두번째 방법, extend
scoresCopy.extend(scores)
print(f'id(scores): {id(scores)}')
print(f'id(scoresCopy): {id(scoresCopy)}')

# 세번째 방법, .copy (리스트 자체 함수)
scoresCopy = scores.copy()
print(f'id(scores): {id(scores)}')
print(f'id(scoresCopy): {id(scoresCopy)}')

# 네번째 방법, [:]
scoresCopy = scores[:]
print(f'id(scores): {id(scores)}')
print(f'id(scoresCopy): {id(scoresCopy)}')

# 다섯번째 방법, 모듈사용
import copy
scoresCopy = copy.copy(scores)
print(f'id(scores): {id(scores)}')
print(f'id(scoresCopy): {id(scoresCopy)}')
```


### 2.7 특수한 이름의 함수("\_\_")

- student를 str()함수의 매개변수로 넣으면 student의 \_\_str\_\_함수가 호출된다
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

### 2.8 비교 연산자의 영어표현
| 이름 | 영어 | 설명 |
| :--: | :-- | :-- |
| eq | equal | 같다 |
| ne | not equal | 다르다 |
| gt | greater than | 크다 |
| ge | greater than or equal | 크거나 같다 |
| lt | less than | 작다 |
| le | less than or equal | 작거나 같다 |

```python
class Student:
  def __init__(self, 이름, 생년월일)
    self.이름 = 이름
    self.생년월일 = 생년월일
  def __eq__(self, other):
    return self.생년월일 == other.생년월일
  def __ne__(self, other):
    return self.생년월일 != other.생년월일
  def __gt__(self, other):
    return self.생년월일 > other.생년월일
  def __ge__(self, other):
    return self.생년월일 >= other.생년월일
  def __lt__(self, other):
    return self.생년월일 < other.생년월일
  def __le__(self, other):
    return self.생년월일 <= other.생년월일
    
student = Student("김재현", 960508)
student == student
student != student
student > student
student >= student
student < student
student <= student
```
True
False
False
True
False
True

### 2.9 ETC
- 프라이빗 변수 : `self.__변수이름` 형태로 선언하여 클래스 내부의 변수를 외부에서 사용하는 것을 막을 수 있다
- 게터(getter) : 프라이빗 변수의 값을 추출한다
- 세터(setter) : 프라이빗 변수의 값을 변경한다
- 데코레이터 : `@property`와 `@<변수이름>.setter`로 더 간단한 형태로 값에 접근아 가능하다

___
## 3. 클래스 상속
- 클래스는 또 다른 클래스를 상속받아 자신의 것처럼 사용할 수 있다.
```
class 클래스명( 기존 클래스 ):
  수정할 내용
```
이미 존재하는 클래스를 물려받아 쓸 때 클래스 상속을 한다.

### 3.1 `super()`
- 클래스의 기능은 상속받으면 바로 사용이 가능하다
- 하지만, 클래스의 속성은 `__init__()`을 호출해야 사용 가능하다
- `super()`을 통해 상속받는 클래스의 속성을 초기화 할 수 있다

```python
class Parent:
  def __inint__(self, pNum1, pNum2)
    print('부모 클래스가 호출되었습니다')
    self.pNum1 = pNum1
    self.pNum2 = pNum2
    
class Child(Parent)
  def __inint__(self, cNum1, cNum2)
    print('자식 클래스가 호출되었습니다')
    
    ## 첫번째 방법
    # Parent.__init__(self, cNum1, cNum2)
    
    ## 두번째 방법
    super().__init__(cNum1, cNum2)
    self.cNum1 = cNum1
    self.cNum2 = cNum2
    
cls = Child(10,20)
```
자식 클래스가 호출되었습니다   
부모 클래스가 호출되었습니다   


___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
