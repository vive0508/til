변수
===

## 1. 변수명
- 영문과 숫자 그리고 \_로 이루어진다.
- 대소문자를 구분한다. 
- 문자나, \_로 시작한다.   
- 특수문자를 사용하면 안된다.
- 키워드를 사용하면 안된다.

### 1.1 대입연산자
```
a = 1
b = 2
c = 3

print(a,b,c)
```
1 2 3

### 1.2 튜플
```
a,b,c = 1, 2, 3

print(a,b,c)
```
1 2 3

___

## 2. 스왑
### case 1. 새로운 변수 사용
```python
a = 10
b = 20
print(a,b)

c = a
a = b
b = c
print(a,b)
```
10 20   
20 10


### case 2. 튜플 사용
```python
a,b = 10,20
print(a,b)

a,b = b,a
print(a,b)
```
10 20   
20 10

- `split()`과 함께 사용
```python
a, b = input().split()
a, b = b, a

print(a)
print(b)
```
