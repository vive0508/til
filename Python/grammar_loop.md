반복문
===
특정한 소스코드를 반복적으로 실해앟고자 할 때 사용하는 문법   
코딩테스트에서는 for문이 더 간결한 경우가 많음   


## 1. for 반복문
### 1.1 기본 문법
```python
for 반복자 in 반복할 수 있는 것:
  실행할 코드
```
### 1.2 리스트에서의 활용
```python
for element in list_sample:
  print(element)
```

### 1.3 딕셔너리에서의 활용
- 키만 활용할 경우
```python
for key in dictionary_sample:
  print(key, ":", dictionary_sample[key])
```

- 키와 값을 모두 활용하는 경우(`딕셔너리.items`)
```python
dictionary_sample = {key1:value1, key2:value2, key3:value3}

for x,y in array.items():
  print(x)
  print(y)
```

### 1.4 범위(range)
- range(a) : 0부터 a-1까지의 정수를 범위로 만듭니다.   
- range(a,b) : a부터 b-1까지의 정수를 범위로 만듭니다.   
- range(a,b,c) : a부터 b-1까지의 정수로 범위를 만드는데, 앞뒤 숫자가 c만큼에 차이를 가집니다.   

### 1.5 기타
```python
for _ in range(5):
  print("Hello World")
```
Python에서 반복을 수행하되 반복을 위한
변수의 값을 무시하고자 할 때, 언더바(_)를 사용한다


## 2. while 반복문
### 2.1 기본 문법
```python
while 조건:
  실행할 코드
```
### 2.2 무한루프 탈출
- if문으로 빠져 나오기
- Ctrl + C 로 강제 종료하기
- break로 빠져 나오기 (for문에서도 사용가능)

### 2.3 `continue` 키워드
- continue를 사용하지 않았을 때
```python
numbers = [5, 15, 6, 20, 7, 25]

for number in numbers:
  if number>=10:
    #문장
    #문장
    #문장
    #문장
    #문장
 ```

- continue를 사용할 때
```python
# 반복 실행중 continue를 만나면 실행을 생략하고, 다음 반복문 실행문으로 넘어간다.
# continue 키워드를 사용하면 조건식으로 다시 돌아가고, 들여쓰기를 하나 줄일 수 있다.

numbers = [5, 15, 6, 20, 7, 25]

for number in numbers:
  if number<10:
    continue
  #문장
  #문장
  #문장
  #문장
  #문장
```

### 2.4 `for/else`
- else의 실행문은 반복문이 종료된 후 실행된다.
```python
cnt = 0
for i in range(100):
  if i % 7 != 0:
    continue
  print('{}는 7의 배수입니다.'.format(i))
else:
  print('99까지의 정수 중 7의 배수는 {}개입니다.'.format(cnt)
```

## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
