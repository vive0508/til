택스트 파일 처리
===
프로그래밍 언어가 외부와 어떻게 소통을 하는지에 초점을 맞출것

## 1. 어떤 대상을   
\- 텍스트 파일 : 텍스트에디터로 열 수 있는 파일
\- 바이너리 파일 : 텍스트에디터로 열 수 없는 파일 (이미지, 동영상, 워드, 엑셀, PDF 등)

### 1.1 텍스트 파일
\- .txt  
\- .csv (comma-separated Values)  
\- .json .xml .YAML  
\- .py .java .html .css .js

___
## 2. 어떻게 다룰 것인가   
### 2.1 모드
\- 쓰기 : 새로 쓰기(write), 있는 파일 뒤에 추가하기(append)
\- 읽기(read)

| 모드 | 의미 |
| --- | --- |
| r | 읽기 전용(파일이 없으면 에러) |
| x | 쓰기 전용(파일이 없으면 에러) |
| w | 쓰기 전용(파일이 있으면 덮어씀) |
| a | 쓰기 전용(파일이 있으면 덧붙여씀) |

| 모드 | 의미 |
| --- | --- |
| rb | read binary |
| wb | write binary |
| ab | append binary |

___
## 3. 인코딩
```python
file = open('cage.txt', 'w', encoding='utf-8')
```
\- 인코딩 : utf-8(유니코드) / cp949 / euc-kr / latin1   
\- 디코딩 : '안녕하세요' => 10111..11011(2)  

___
## 3. `open()` & `close()`
```python
file = open('test.txt', 'a')
file.write('hello world!')
file.close()

file = open('test.txt', 'r')
print(file.read())
file.close()
```

## 4. with 구문
```python
with open('test.txt', 'a') as file:
   실행시킬 코드
```
`close()`를 따로 입력하지 않아도 되는 구문이다

## 5. writelines()
- 반복 가능한 자료형의 데이터 파일에 쓴다
```python
# practice 1
languages = ['kor','eng','jpn']

uri = 'C:/pythonPratice/'
with open(uri + 'languages.txt', 'a') as f:
   f.writelines(item + '\n' for item in languages)

# practice 2
Scores= {'kor':100 ,'eng'=90 ,'jpn'=85}

uri = 'C:/pythonPratice/'
with open(uri + 'scores.txt', 'a') as f:
   f.write(key + '\t:' + str(scores[key] + '\n')
```

## 6. readlines(), readline()
- `readlines` : 여러 줄 읽기
```python
uri = 'C:/pythonPratice/'

with open(uri + 'languages.txt', 'r') as f:
   languages = f.readlines()
   
print(f'languages : {languages}')
print(f'languages type : {type(languages)}')
```
languages : ['kor', 'eng', 'jpn']   
languages type : <class 'list'> 

- `readline` : 한줄 읽기
- ```python
uri = 'C:/pythonPratice/'

with open(uri + 'languages.txt', 'r') as f:
   languages = f.readline()
   
    while line != '':
      print(f'line: {line}', end='')
      line = f.readline()
```
line : kor   
line : eng
line : jpn   

___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
