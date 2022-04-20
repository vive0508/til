파일처리
===

### 1. 파일 / 모드 / 인코딩

- open(파일, 모드)
```python
file = open('cage.txt', 'w', encoding='utf-8')
```

- close()
```python
file.close()
```
open 이후에는 반드시 close를 해주어야 한다

#### 1.1. 텍스트 파일
\- .txt  
\- .csv (comma-separated Values)  
\- .json .xml .YAML  
\- .py .java .html .css .js

#### 1.2 모드
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

#### 1.3 인코딩, 디코딩
\- Unicode
\- '안녕하세요' => 10111..11011(2)  
\- utf-8 / cp949 / euc-kr / latin1
\- 위의 방법으로도 파일이 열리지 않으면 텍스트 파일을 메모장으로 열고난 후 다른 이름으로 저장하면서 encoding


### 2. with 구문
```python
with open("파일","모드") as sth:
    문장
```
close를 따로 입력하지 않아도 되는 구문

___
## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
* [이것이 취업을 위한 코딩 테스트다 with 파이썬(나동빈)](https://www.hanbit.co.kr/store/books/look.php?p_code=B8945183661)
