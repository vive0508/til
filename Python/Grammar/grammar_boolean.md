불 자료형
===
불은 오직 True(참)와 False(거짓)값만 가질 수 있다.

## 1. 연산자
### 1.1 비교 연산자
| 연산자 | 의미 |
| :--: | :--: |
| \== | 같다 |
| != | 다르다 |
| < | 작다 |
| \> | 크다 |
| <= | 작거나 같다 |
| \>= | 크거나 같다 |

### 1.2 논리 연산자
| 연산자 | 의미 |
| :--: | :--: |
| not | 아니다 |
| and ( & ) | 그리고 |
| or ( \| ) | 또는 |

### 1.3  `all`, `any`
- all은 괄호 안에 있는 조건이 모두 참이어야 True를 반환
```python
a = [9, 30, 40, 50, 20]

if all(10<x for x in a):
  print('yes')
else:
  print('no')
```
no

- any는 괄호 안에 있는 조건이 하나라도 참이면 True를 반환
```python
a = [9, 30, 40, 50, 20]

if any(10>x for x in a):
  print('yes')
else:
  print('no')
```
yes

### 1.4 in 연산자
- x in _문자열/리스트/딕셔너리.keys()/딕셔너리.values()..._   
- x not in _문자열/리스트/딕셔너리.keys()/딕셔너리.values()..._

___
## 2. 기타
- True : 0이 아닌 모든 수, 비어있지 않은 모든 그룹형 변수
- False : 0이거나 비어있는 모든 그룹형 변수

```
int(True) -> 1
float(True) -> 1.0
int(False) -> 0
float(False) -> 0.0
```

## 3. 형변환
```python
# 문자형 자료형
str1 = 'False'
print(type(str1))
print(str1)

# 문자형 자료형 → 불 자료형
str1 = bool(str1)
print(type(str1))
print(str1)

# 불 자료형의 산술연산
print(str1+str1)
```
<class 'str'>   
False   
<class 'bool'>   
True   
2


## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
