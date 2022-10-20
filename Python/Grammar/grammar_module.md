모듈
===

## 1. 모듈의 종류
### 1.1 표준 모듈 (내장 모듈)
파이썬에 기본적으로 내장되어 있는 모듈    
표준모듈에 대한 정보는 [파이썬 공식 문서](https://docs.python.org/3/library/index.html)를 확인한다

#### 1.1.1 구문
- from 구문
```python
from 모듈 이름 import 가져오고 싶은 변수 또는 함수
```
- as 구문
```python
import 모듈 as 사용하고 싶은 식별자
```

#### 1.1.2 math 모듈 : 수학 관련 모듈
```python
# math = __import__("math")
import math

print(math.pi)
print(math.sin(10))
```
| 변수 또는 함수 | 설명 |
| :--: | :-- |
| sin(x) | 사인값을 구합니다 |
| cos(x) | 코사인값을 구합니다 |
| tan(x) | 탄젠트값을 구합니다 |
| log(x[, base]) | 로그값을 구합니다 |
| ceil(x) | 올림합니다 |
| floor(x) | 내림합니다 |
| round(x) | 반올림합니다 |
| trunc(x) | 뒤의 소수점을 버립니다 |
| fabs(x) | 절댓값을 구합니다 |
| gcd(a,b) | 최대공약수를 구합니다 |
| factorial(x) | 팩토리얼을 구합니다 |
| sqrt(x) | 제곱근을 구합니다 |

#### 1.1.3 random 모듈 : 난수 관련 
랜덤한 값을 생성할 때 사용하는 모듈
```python
import random

# 0.0~1.0 사이의 float을 리턴한다
print(random.random())

# 지정한 범위 사이의 float를 리턴한다
print(random.uniform(min, max))

# 지정한 범위의 int를 리턴한다
print(random.randint(min, max))
print(random.randrange(max))
print(random.randrange(min, max))

# 지정한 범위의 난수 k개를 발생시킨나
print(random.sample(range(min, max), k)

# 리스트 내부에 있는 요소들을 랜덤하게 선택한다
print(random.choice([1, 2 ,3 ,4]))

# 리스트의 요소를 랜덤하게 섞는다
print(random.shuffle([1, 2, 3, 4, 5]))

# 리스트의 요소 중에서 랜덤하게 k를 뽑는다
print(random.shuffle([1, 2, 3, 4, 5], k=2))
```

#### 1.1.4 sys 모듈
시스템과 관련된 정보를 가지고 있는 모듈
```python
import sys

# 파이썬 버전
print(sys.version)

# 파이썬 카피라이트
print(sys.copyright)

# 명령 매개변수(arguments value)
print(sys.argv)
```

#### 1.1.5 os 모듈
운영체재와 관련된 모듈
```python
import os

# 현재 운영체제
print(os.name)

# 현재 폴더
print(os.getcwd())

# 현재 폴더 내부의 요소
print(os.listdir())

# 파일 생성 및 이름 변경
with open("original.txt", "w") as file:
  file.write("hello")
os.rename("original.txt", "new.txt")

# 파일 제거
os.remove("new.txt")
```

#### 1.1.6 datetime 모듈
날짜(date), 시간(time)과 관련된 모듈
```python
# import datetime
# datetime.datetime.now()

from datetime import datetime

print(now = datetime.now())
print(now.year)
print(now.month)
print(now.day)
print(now.hour)
print(now.minute)
print(now.second)
```

#### 1.1.7 time 모듈 : 시간 관련 모듈
시간과 관련된 모듈
```python
import time

# 로컬의 시간
time.localtime()
lt = time.localtime()

lt.tm_year
lt.tm_mon
lt.tm_mday
lt.tm_hour
lt.tm_min
lt.tm_sec
lt.tm_wday

# 일시정지
time.sleep(5)
```

#### 1.1.8 urllib 모듈
URL을 다루는 라이브러리
```python
from urllib import request

source = request.urlopen()
content = target.read()
```

#### 1.1.9 operator 모듈
- 산술연산자   

| 연산자 | 함수 |
| :--: | :-- |
| + | operator.add(num1, num2) |
| - | operator.sub(num1, num2) |
| * | operator.mul(num1, num2) |
| / | operator.truediv(num1, num2) |
| % | operator.mod(num1, num2) |
| // | operator.floordiv(num1, num2) |
| ** | operator.pow(num1, num2) |

- 비교연산자   

| 연산자 | 함수 |
| :--: | :-- |
| == | operator.eq(num1, num2) |
| != | operator.ne(num1, num2) |
| > | operator.gt(num1, num2) |
| >= | operator.ge(num1, num2) |
| < | operator.lt(num1, num2) |
| <= | operator.le(num1, num2) |

- 논리연산자 (flag1=True, flag2=False) 
  
| 연산자 | 함수 |
| :--: | :-- |
| and | operator.and_(flag1, flag2) |
| or | operator.or_(flag1, flag2) |
| not | operator.not_(flag1) |

___
### 1.2 외부 모듈 (외장 모듈)
- 파이썬에 내장되어 있지 않아서, 별도로 다운 받아서 사용하는 모듈
```python
# pip install 모듈이름==1.0.0
pip install 모듈이름
```
- 패키지 : 모듈이 모인것

#### 1.2.1 대표 외부 모듈
- 웹 서버 개발 : Flask, Django
- 인공지능 개발 : scikit-learn, tensorflow, keras
- 데이터분석 : pandas, matplotlib
- 크롤러 개발 : BeautifulSoup, requests, scrapy

#### 1.2.2 라이브러리, 프레임워크   
- 라이브러리   
개발자들이 모듈의 기능을 호출하는 형태와 같이 정상적인 제어를 하는 모듈   

- 프레임워크   
제어 역전이 일어나는 모듈

- 제어역전(IoC, Inverse of Control)   
개발자가 모듈의 함수를 호출하는 것이 일반적인 제어 흐름이나, 이와 반대로 개발자가 만든 함수를 모듈이 실행하는 것을 말한다

#### 1.2.3 모듈 만들기
- 한 파일의 크기가 너무 커졌을 때 모듈을 만들어 분리한다
```python
# my_module.py
a = 10
b = 20
def c() :
  retrun 30
```
```python
# 다른 폴더에 있다면 import 폴더/폴더/파일
import my_module

my_module.a
my_module.b
my_module.c()
```
10   
20   
30   

- 현재 실행되고 있는 파일의 위치 확인 : `__name__`
```python
# my_module.py
print(__name__)

a = 10
b = 20
def c() :
  retrun 30
```
```python
# 엔트리 포인트, 메인파일은 `__name__` 사용 시 `__main__`으로 리턴된다
print(__name__)
import my_module
my_module.a
my_module.b
my_module.c()
```
\_\_main\_\_   
my_module   
10   
20   
30   

## 2. 패키지
- 패키지로 모듈을 그룹으로 관리할 수 있다
```python
import sys

for path in sys.path:
  print(path)
```
C:\ooo\ooo\venv\lib\site-packages

- 패키지를 site-packages로 옮기면 어디에서나 패키지를 사용할 수 있다   
___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
