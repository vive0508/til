## 파이썬 두 변수의 값 바꾸기 (Swap)
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

___
## ○ 코드업 기초 100제
* [코드업 기초 100제](https://codeup.kr/index.php)
