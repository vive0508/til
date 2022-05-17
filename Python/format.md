## `format()` 함수
___
### 1. 진수변환 

```python
dNum = int(input('정수를 입력해주세요: '))
print('2진수 :{}'.format(format(dNum, '#b')))
print('8진수 :{}'.format(format(dNum, '#o')))
print('16진수 :{}'.format(format(dNum, '#x')))
```

### 2. 반올림
- format(수, ".2f") 를 사용하면 원하는 자리까지의 정확도로 반올림 된 실수 값을 만들어 준다.
```python
a=float(input())
print(format(a,".2f"))
```
- 연산을 활용하는 것도 가능하다
```python
f1, f2 = input().split()

f1 = float(f1)
f2 = float(f2)

print(format(f1/f2, ".3f"))
```
파이썬에서 실수가 컴퓨터로 저장되는 과정에 잘림(truncation) 오차가 발생한다.   
그래서 실수 변환이나 실수를 사용하는 계산은 모두 근사값으로 계산되는 것이라고 할 수 있다.   

### 3. 세 자리수 구분
```python
money = 10000
strMoney = format(money ,',')
print(strMoney)
```
10,000
___
## ○ 코드업 기초 100제
* [코드업 기초 100제](https://codeup.kr/index.php)
