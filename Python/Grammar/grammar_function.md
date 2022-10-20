함수
===

## 1. 함수
### 1.1. 함수란?
- 함수란 특정한 작업을 하나의 단위로 묶어놓은 것
- 함수를 사용하면 불필요한 소스코드의 반복을 줄일 수 있다
- 함수의 시야(Scope) : 함수 안에 있는 문장의 내용은 함수 안에서만 존재한다.
___
### 1.2 내장 함수 : 파이썬이 기본적으로 제공하는 함수
#### 1.2.1 출력: `print()`
- 괄호 안에 있는 메시지를 출력한다
- 괄호 안에 아무것도 입력이 되어있지 않으면 빈줄이 출력되어 줄바꿈이 된다.
- 콤마(,)를 붙여 여러 개를 출력할 수 있다.
- 괄호 안에 콤마(,)와 함께 end=""를 입력하면 가로로 출력할 수 있다

#### 1.2.2 사용자 입력: `input()`
- 괄호 안에 입력한 프롬프트 문자열이 사용자로부터 입력을 요구한다.
- 사용자가 입력하기 전까지 프로그램이 잠시 멈춘다. 이를 블록이라 한다.
- input 함수의 결과는 무조건 문자형 자료형이다.
___
### 1.3 사용자 정의 함수 : 개발자가 직접 정의하여 사용할 수 있는 함수
```python
def 함수이름 ():
  실행할 코드
```
- 전역변수, 지역변수
\- 함수 밖에서 선언된 변수로, 함수 밖에서나 안에서나 모두 사용 가능하다.   
\- 지역변수 : 함수 안에서 선언된 변수로 함수 안에서만 사용 가능하다.
```python
# 함수 안의 num은, 함수 밖의 num과는 다른 새로운 지역변수
num = 10
def printNum():
  num = 20
  print(num)
  
printNum()
print(num)
```
20   
10   


- `global`키워드
함수 밖에 선언된 변수(전역변수)는 어디에서나 사용은 가능하지만 함수 안에서 수정은 할 수 없다.   
만약 함수 안에서 전역변수의 수정을 원할 경우에는 global 키워드를 사용한다.

```python
a = 0

def func():
  global a
  a += 1
  
for i in range(10)
  func()

print(a)
```
10

___
### 1.4 매개변수(parameter)
- 외부에 있는 변수를 활용할 때는 매개변수(parameter)에 인수(argument)를 넣어줘야 한다
- 이때 말하는 parameter는 통계, ML, DL에 나오는 parameter와는 다른 개념


#### 1.4.1 가변 매개변수

- 매개변수를 원하는 만큼 받을 수 있는 함수
- 가변 매개변수 뒤에는 일반 매개변수가 올 숭 없다
- 가변 매개변수는 하나만 사용할 수 있다

```python
def 함수이름(매개변수1, 매개변수2, *가변 매개변수):
  print(매개변수1)
  print(매개변수2)
  print(가변매개변수)

함수이름(0,1,2,3,4,5,6,7,8,9)
```
0   
1   
(2, 3, 4, 5, 6, 7, 8, 9)


#### 1.4.2 기본 매개변수
- 매개변수를 입력하지 않을 경우 매개변수에 들어가는 기본값
- '매개변수=값'의 형태로 되어있음
- 기본 매개변수 뒤에는 일반 매개변수가 올 수 없다.

```python
def print_n_times(value, n=5):
  for i in range(n)
    print(value)

print_n_times("안녕하세요")
```
안녕하세요   
안녕하세요   
안녕하세요   
안녕하세요   
안녕하세요   

#### 1.4.3 키워드 매개변수
- 일반 매개변수 - 가변 매개변수 - 기본 매개변수 순서로 매개 변수를 선언한다
```python
def function(일반매개변수A, 일반매개변수B, *가변매개변수, 기본매개변수A=10, 기본매개변수B=20):
  print(일반매개변수A, 일반매개변수B)
  print(가변매개변수)
  print(기본매개변수A, 기본매개변수B)

function(0,1,2,3,4,5,6,7,8,9,10, 기본매개변수B=12)
```
0 1   
(2,3,4,5,6,7,8,9,10)   
10 12   


___
### 1.5 반환값(return)
#### 1.5.1 리턴
- 함수안의 print()함수의 결과값은 휘발된다.
```
def add(a,b):
    result = a+b
    print(result)
    
x = add(3,2)
print(x)
```
none

- 반면, return으로 반환된 결과값은 함수실행 이후에도 활용 가능하다.
```
def add(a,b):
    result = a+b
    return result
    
x = add(3,2)

print(x)
```
5

- 일반적으로 덧셈에서는 초깃값을 0으로, 곱셈에서는 초깃값을 1으로 설정  
```python
def 함수(매개변수):
  변수 = 초깃값
  # 여러 가지 처리
  # 여러 가지 처리
  # 여러 가지 처리
  return 변수
```
- 파이썬에서 함수는 여러 개의 반환 값을 가질 수 있다
```python
def operator(a,b):
  add_var = a+b
  subtract_var = a-b
  multiply_var = a*b
  divide_var = a/b
  return add_var, subtract_var, multiply_var, divide_var

# 반환값이 여러 개인 경우 튜플의 형태로 반환된다.
print(operator(7,3))

# 튜플의 기능을 활용하여 변수에 값을 할당할 수 있다.
a, b, c, d = operator(7,3)
print(a, b, c, d)
```
(10, 4, 21, 2.3333333333333335)   
10 4 21 2.3333333333333335


#### 1.5.2 조기리턴
- return이 되면 함수가 종료된다.
```
# 소수를 찾는 프로그램을 만든다.

def isPrime(x):
  for i in range(2,x):
    if x%i==0:
      return False
  return True
  
a = [12, 13, 7, 9, 19]
for i in a:
  if isPrime(i):
    print(i, sep=',' end=' ')
```
13 7 19

- 자세한 내용은 하단 2.3 조기리턴 참고



___
### 2. 함수의 활용
#### 2.1 재귀함수
재귀함수는 자기자신을 호출하는 함수   
함수 내부에서 함수를 호출하는 함수

##### 2.1.1 팩토리얼
- case 1
```python
# n! = 1*2*3*(n-2)*(n-1)*n

def factorial_1(n):
  변수 = 1
  for i in range(1, n+1)
    변수 *= i
  return 변수
```

- case 2
```python
# 0! = 1
# n! = n*(n-1)!

def facorial_2(n):
  if n == 0 :
    return 1
  else:
    retrun n * factorial(n-1)
```

___
#### 2.2 메모화
##### 2.2.1 피보나치 수열
- 재귀함수로 구현했을 경우
```python
# f(1) = 1
# f(2) = 1
# f(n) = f(n-1) + f(n-2)

counter = 0

def f(n)
  global counter =+ 1
  if n==1 or n==2:
    return 1
  else:
    return f(n-1) + f(n-2)

print(f(35))
print(counter)
```
9227465   
18454929   
   
![메모화](https://user-images.githubusercontent.com/101171109/164179205-23961c1c-c4c7-457f-864d-f808fd1e5429.png)   
이미 구했던 값을 여러번 반복해서 구하는 문제가 생겨 연산의 시간이 길어진다  

- 메모화를 사용했을 경우
``` python
메모 = {1:1, 2:1}

def f(n):
  if n in 메모 :
    return 메모[n]
  else:
    output = f(n-1) + f(n-2)
    메모[n] = output
    return output
    
print(f(150))
```
9969216677189303386214405760200    
이전과 달리 빠른 속도로 연산이 됨

___

#### 2.3 조기리턴
``` python
메모 = {1:1, 2:1}

def f(n):
  if n in 메모 :
    return 메모[n]
  output = f(n-1) + f(n-2)
  메모[n] = output
  return output
    
print(f(150))
```
들여쓰기 단계가 줄어 코드를 더 쉽게 읽을 수 있다   
이렇게 흐름 중간에 return 키워드를 사용하는 것을 조기리턴이라고 한다   

___
## 3. 튜플
리스트와 비슷한 자료형이지만 다음과 같은 차이가 있음
1. 대괄호가 아니라 소괄호로 선언
2. 한 번 선언하면 값을 바꿀 수 없어, 키 값으로 사용될 수 있다
  (아템 추가, 변경, 삭제가 불가하다)
3. 리스트에 비해 상대적으로 공간 효율적이다
4. 리스트와 튜플은 자료형 변환이 가능하다 `list()`, `tuple()`

### 3.1 튜플 접근
- 튜플 요소에 접근하는 방법
```python
tuple_sample = (10, 20, 30)

tuple_sample[0]
tuple_sample[1]
tuple_sample[2]
```
10   
20   
30   


### 3.2 튜플을 사용하는 경우
#### 3.2.1 복합할당
- 일반적인 할당하는 방법
```python
[a, b] = [10, 20]
(c, d) = (30, 40)

print(a,b,c,d)
```
10 20 30 40   

- 괄호가 없어도 튜플로 인식될 수 있다면 튜플 (선언 시 괄호 생략 가능)
```python
tuple_sample = 10, 20, 30, 40
print("tuple_sample:", tuple_sample)
print("type(tuple_sample):", type(tuple_sample))
```
tuple_sample: (10, 20, 30, 40)   
type(tuple_test): <class 'tuple'>   

#### 3.2.2 스왑
```python
a, b = 10, 20

print(a,b)
a,b = b,a
print(a,b)
```
10 20   
20 10   

#### 3.2.3 튜플을 리턴하는 함수
- 예시 1   
```python
def test():
  return 10, 20

a, b = test()
print(a, b)
```
10 20


- 예시 2   
```python
a, b = 97, 40
print(divmod(a,b))
```
(2, 17)

- 예시 3   
```python
for i, value in enumerate([1, 2, 3, 4, 5, 6]):
  print("{}번째 요소는 {}입니다".format(i, value))
```
0번째 요소는 1입니다   
1번째 요소는 2입니다   
2번째 요소는 3입니다   
3번째 요소는 4입니다   
4번째 요소는 5입니다   
5번째 요소는 6입니다   

### 3.3 튜플 관련 내용
#### 3.3.1 요소 하나를 가지는 튜플
```python
(273, )
```

#### 3.3.2 딕셔너리에 키로 사용가능
딕셔너리 키에는 리스트는 사용불가   
그 이외 튜플을 포함한 다른 자료형은 사용가능

```python
dict = {
  (0, 0) : 10,
  (0, 1) : 20,
  (1, 0) : 30,
  (1, 1) : 40
  
print( dict[(0,0)] )
print( dict[0,0] )
}
```
10   
10

#### 3.3.3 튜플의 결합
- 리스트에서 사용할 수 있는 extend()함수는 튜플에서 사용할 수 없다.
```python
tuple_1 = (1, 2, 3)
tuple_2 = (4, 5, 6)

tuple_3 = tuple_1+tuple_2
print(tuple_3)
```
(1, 2, 3, 4, 5, 6)

- 튜플에 요소 추가하는 방법
```python
num1 = (1, 3, 5, 7)
num2 = (2, 4, 6)

for i in num2:
  if i not in num1:
    num1 = num1 + (i, )

print(num1)
```
(1, 3, 5, 7, 2, 4, 6)

#### 3.3.4 튜플 슬라이싱
- 인덱스 활용
- `slice()` 함수

#### 3.3.5  튜플의 정렬
1. 리스트로 변환 후 정렬 : list() → sort() → tuple()
2. `sorted()` 함수 활용 : 튜플을 정렬하여 리스트로 만드는 함수

#### 3.3.6 내부 튜플 조회
```python
players = ( ('수비', '김민재'), ('미드필더', '황인범'), ('공격수', '황희찬') )
for position, player in players:
   print('{} 포지션 : {}'.format(position, player))
```
수비 포지션 : 김민재   
미드필더 포지션 : 황인범   
공격수 포지션 : 황희찬

___
## 4. 람다
함수라는 기능을 매개변수로 전달하는 코드를 사용한다   
파이썬은 이를 위해 람다(lamda)라는 기능을 제공한다

### 4.1 예제
#### 4.1.1 예제 1
- 콜백함수를 사용했을때

```python
# 내가 함수를 호출하는 것이 아니라,   
# 함수가 함수를 호출하는 것을 콜백함수라고 한다

def call_5_times(func):
  for i in range(5):
    func(i)

def print_hello(number):
  print("안녕하세요", number)

call_5_times(print_hello)
```
안녕하세요 0   
안녕하세요 1   
안녕하세요 2   
안녕하세요 3   
안녕하세요 4   


- 람다를 사용했을때
```python
# 함수(lamda 매개변수 : 한줄 코드)

def call_5_times(func):
  for i in range(5):
    func(i)
    
call_5_times(lambda number: print("안녕하세요", number))
```
안녕하세요 0   
안녕하세요 1   
안녕하세요 2   
안녕하세요 3   
안녕하세요 4   

#### 4.1.2 예제 2
- 함수를 사용했을때
```python
def plus_one(x):
        return x+1
print(plus_one(1))
```
2
- 람다를 사용했을 때
```python
plus_one=lambda x:x+1
print(plus_one(1))
```
2

#### 4.1.3 예제 3
- 함수를 사용했을때
```python
def plus_one(x):
        return x+1

a=[1,2,3]
print(list(map(plus_one,a)))
```
[2, 3, 4]
- 람다를 사용했을 때
```python
a=[1,2,3]
print(list(map(lambda x:x+1,b)))
```
[2, 3, 4]

___

### 4.2 중첩함수(cf. 콜백함수)
- 중첩함수 : 함수 안에 또 다른 함수가 있는 형태
```python
def out_function():
  print('out_function 입니다')
  
  def in_function():
    print('in_function 입니다')
    
  in_function()

out_function()
```
out_function 입니다   
in_function 입니다

- 중첩함수의 내부 함수는 함수 밖에서 호출할 수 없다.
```python
def out_function():
  print('out_function 입니다')
  
  def in_function():
    print('in_function 입니다')
    
  in_function()

in_function()
```
NameError: name 'in_function' is not defined


### 4.3 표준 함수 (= 내장함수)
- 함수를 매개변수로 전달하는 대표적인 표준함수로 `map()`과, `filter()`가 있다.


#### 4.3.1 `fileter(fun, *iterables)`
리스트의 요소를 함수에 넣고, 리턴된 값이 True인 것으로 새로운 리스트를 구성해주는 함수

- filter() 함수
```python
def 짝수만(number):
  return number % 2 == 0

a = list(range(10))
b = filter(짝수만, a)

print(list(b))
for i in b:
  print(i)
```
[0, 2, 4, 6, 8}   
0   
2   
4   
6   
8   

- filter() 함수 with 람다
```python
a = list(range(10))
b = filter(lambda number: number % 2 == 0, a)

print(list(b))
for i in b:
  print(i)
```
[0, 2, 4, 6, 8}   
0   
2   
4   
6   
8   


#### 4.3.2 `map(function or None, iterable)`
리스트의 요소를 함수에 넣고, 리턴된 값으로 새로운 리스트를 구성해주는 함수

- `map()`함수
```python
def 제곱(number):
  return number * number

a = list(range(5))
print(list(map(제곱, a)))
```
[0, 1, 4, 9, 16, 25]

- `map()`함수 with 람다
```python
a = list(range(5))
print(list(map(lambda number : number * number, a)))
```

- `map()`함수 활용
```python
a, b, c = map(int, input().split())
a, b, c = map(float, input().split())
```

### 4.4 리스트 내포와 비교하기
```python
a = list(range(5))
print([i*i for i in a if i % 2 == 0])
```
`map()`,`filter()` 함수는 제너레이터 함수라서   
내부의 데이터가 실제로 메모리에 용량을 차지하지 않는다   
하지만 신경쓰지 않을 정도로 컴퓨터의 성능이 매우 발전   
최근에는 리스트내포 구문이 많이 쓰이는 추세이다   


___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
