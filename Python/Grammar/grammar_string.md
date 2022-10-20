문자열 자료형
===

## 1. 문자열 자료형
- 큰따옴표로 문자열을 만들 수 있다.
- 작은따옴표로 문자열을 만들 수 있다.
- 문자열 내부에 따옴표를 넣을 때는 하기의 방법을 이용한다.

```
print("'안녕하세요'라고 말했습니다")
print('"안녕하세요"라고 말했습니다')
print("\"안녕하세요\"라고 말했습니다")
print('\'안녕하세요\'라고 말했습니다')
```

## 2. 형변환(Cast)
- `str()` : 매개 변수에 다른 자료형을 넣으면 값을 문자열로 변환 할 수 있다.

## 3. 문자열 연산자

| 기능 | 연산자 |
| --- | --- |
| 문자열 연결 연산자 | + |
| 문자열 반복 연산자 | \* |
| 문자 선택 연산자 | \[\] |

문자열 내부 특정 한글자를 변경하는 것은 불가능

## 4. 이스케이프 문자열

| 이스케이프 문자 | 기능 |
| :--: | :-- |
| \\" | 큰따옴표 |
| \\' | 작은따옴표 |
| \\n | 줄바꿈 |
| \\t | 탭 |
| \\\\ | 역슬래시 \\ |



## 5. 문자열 관련 함수
### 5.1 `split()`
문자열을 특정문자로 잘라서 리스트로 만들 때 사용

```python
print("10 20 30 40 50".split(" "))
```
['10', '20', '30', '40', '50']

### 5.2 `list(map(int, input().split())`
```
a, b, c = map(int, input().split())
print(a,b,c)
```
입력 >>> 1 2 3   
출력 >>> 1 2 3

```
sample_list = list(map(int, input().split()))
print(sample_list)
```
입력 >>> 1 2 3   
출력 >>> [1, 2, 3]


### 5.2 `join()` 
함수리스트의 요소를 문자열로 연결할 때 사용
```python
print("::".join(['10','20','30','40','50'])
```
10::20::30::40::50

### 5.3 `upper()`, `lower()`
```python
word = 'Python'
print(word.upper()) # 대문자
print(word.lower()) # 소문자
print(word) # 비파괴적
```
PYTHON   
python   
Python   


### 5.4 `find()`, `count()`
```python
sentence = 'Python is good'
print(sentence.find('o')) # 인덱스 번호 (첫번째만)
print(sentence.count('o')) # 찾는 문자의 갯수
```
4   
3   

### 5.5 `isupper()`, `islower()`, `isalpha()`
```
sentence = 'Today I Learned'

# isupper
for i in sentence:
  if i.isupper():
    print(i, end='')

print()

# islower
for i in sentence:
  if i.islower():
    print(i, end='') 
    
print()

# isalpha
for i in sentence:
  if i.isalpha():
    print(i, end='') 
```
TIL   
odayearned   
TodayILearned

### 5.6 아스키 코드 (ASCII Code)
#### 5.6.1 문자 → 10진수 유니코드 변환
```python
# ord()는 문자->정수값  
c = input()
print(ord(c))
```
#### 5.6.2 정수 → 유니코드 문자 변환
```python
# chr()는 정수값->문자   
c = int(input())
print(chr(c))
```

#### 5.6.3 문자 1개를 입력받아 다음 문자 출력
```python
c = input()
c = chr(ord(c)+1)
print(c)
```

___

## 6. 문자열 포맷팅
문자열 중간에 변수의 값을 넣어주기 위한 방법   
포매팅에 대한 자세한 설명은 블로그 링크로 대체

- format()함수 [링크](https://blockdmask.tistory.com/424)
```python
# format 함수의 인덱스 활용
print('인덱스를 활용하여 {1}를 첫번째 자리에, {0}를 두번째 자리에 입력할 수 있습니다.'.format('첫번재 변수', '두번째 변수'))
```
인덱스를 활용하여 두번째 변수를 첫번째 자리에, 첫번재 변수를 두번째 자리에 입력할 수 있습니다.
```python
# format을 다음과 같이 사용하는 것도 가능합니다. 
hello = "안녕하세요, {name}입니다"
hello.format(name="김재현")
```

- % 포매팅 [링크](https://blockdmask.tistory.com/428)   

| 형식 문자 | 자료형 |
| :--: | :--: |
| %s | 문자열 |
| %d | 정수 |
| %f | 실수 |

```
# 소수점 자리수 정하기 (%.nf)
print('Pi : %.0f' % 3.141592)
print('Pi : %.1f' % 3.141592)
print('Pi : %.2f' % 3.141592)
```
Pi : 3   
Pi : 3.1   
Pi : 3.14

- f-string [링크](https://blockdmask.tistory.com/429)
```
a = 1
b = 2

print(f'{a}와 {b}를 더하면 {a+b}이(가) 됩니다')
```
1와 2를 더하면 3이(가) 됩니다


## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
