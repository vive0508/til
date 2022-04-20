파일처리
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
| r | read |
| w | write |
| a | append |
   
| 모드 | 의미 |
| --- | --- |
| rb | read binary |
| --- | --- |
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

## 4. `with 구문`
```python
with open('test.txt', 'a') as file:
   실행시킬 코드
```
`close()`를 따로 입력하지 않아도 되는 구문이다


___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
