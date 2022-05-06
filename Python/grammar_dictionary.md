딕셔너리 자료형
===
리스트나 튜플이 값을 순차적으로(인덱스) 저장하는 것과는 달리   
딕셔너리는 키와 값의 쌍을 데이터로 가지는 자료형이다.   
변경 불가능한(Immutable) 자료형을 키로 사용할 수 있다.   

## 1. 딕셔너리
### 1.1 딕셔너리 접근
`dict[키]` : 입력한 키에 해당하는 값이 나온다   
`dict.get[키, 디폴트값]` : 입력한 키에 해당하는 값이 나오고, 없을 경우 디폴트 값이 나온다   
`keys()` : 딕셔너리의 키만 추출   
`values()` : 딕셔너리의 값만 추출   
`dict.items()` : 키와 값을 모두 활용

```python
dictionary_sample = {key1:value1, key2:value2, key3:value3}

for x,y in array.items():
  print(x)
  print(y)
```

### 1.2 딕셔너리 추가
```python
dict[키] = 값
```
만약 기존의 존재하는 키를 지정하고 값을 넣으면 새로운 값이 이를 대체한다.

### 1.3 딕셔너리 제거
- 해당 키와 값이 모두 제거
```python
del 딕셔너리명[키]
딕셔너리명.pop('키')
```
- 모든 키와 값이 모두 제거
```python
딕셔너리명.clear()
```


## ○ 레퍼런스
* [혼자 공부하는 파이썬(윤인성)](https://www.hanbit.co.kr/store/books/look.php?p_code=B2587075793)
* [이것이 취업을 위한 코딩 테스트다 with 파이썬(나동빈)](https://www.hanbit.co.kr/store/books/look.php?p_code=B8945183661)
