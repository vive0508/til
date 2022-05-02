## 유니코드
컴퓨터로 저장되고 처리되는 모든 데이터들은 2진수 형태로 정수화 되어야 하는데,   
컴퓨터에 문자를 저장하는 방법으로 아스키코드(ASCII Code)나 유니코드(Unicode)가 자주 사용된다.   

___
### `ord()`함수
#### 1. 문자 → 10진수 유니코드 변환
```python
# ord()는 문자->정수값  
c = input()
print(ord(c))
```
#### 2. 정수 → 유니코드 문자 변환
```python
# chr()는 정수값->문자   
c = int(input())
print(chr(c))
```

#### 3. 문자 1개를 입력받아 다음 문자 출력
```python
c = input()
c = chr(ord(c)+1)
print(c)
```
___
## ○ 코드업 기초 100제
* [코드업 기초 100제](https://codeup.kr/index.php)
