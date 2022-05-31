정형 데이터 분석
===

### 데이터 분석를 위한 라이브러리

| **라이브러리명** | **용도** | **별칭** | **import 구문 예시** |
| --- | --- | --- | --- |
| \*numpy | 수치형 자료 계산 및 연산 | np | import numpy as np |
| \*pandas | 정형 데이터 전처리 및 분석 | pd | import pandas as pd |
| \*matplotlib | 데이터 차트 시각화 | plt | import matplotlib.pyplot as plt |
| seaborn | 보다 개선된 데이터 시각화 | sns | import seaborn as sns |
| beautifulsoup4(bs4) | 웹 데이터 추출(web scraping) |   | from bs4 import ~~ |
| nltk | 자연어 데이터 전처리 |   | import nltk |
| scikit-learn | 전통적인 머신러닝 알고리즘 |   | from sklearn import ~~ |

---

### 데이터의 구분

- 정형데이터 : 엑셀처럼 행과 열이 있는 데이터 (Tranditional ML)
- 반정형 데이터 : 비정형 데이터에 있는 텍스트의 일종, 다만 규격이 있음 (HTML, 로그)
- 비정형 데이터 : 이미지, 영상, 음성 (딥러닝 많이 사용)
\*\* 표형태의 데이터(tabular data)에도 성능이 잘 나오는 딥러닝 기술들이 개발되고 있음

### 모듈
- .py파일로 모듈을 만든다.
- import로 모듈명/파일명을 불러들인다.
- 모듈명.함수명()
- 기능별로 나눠서 관리할 때 좋음
- 주피터 노트북 옆에 파이썬 파일이 있어야 함
- 파이선 파일이 많아지면 복잡해짐

### 라이브러리
- Library, Package라고 불림
- Module(단일.py)의 상위 개념

### import 구문

- import 라이브러리이름 as 별명
- from 라이브러리이름 import 함수이름
  - 함수 이름에 \*는 와일드 카드
  - \* : wild-card == whole (all)

___

# pandas : 정형 데이터 전처리 및 분석

## 1. 원본 데이터 세팅

### 1.1 라이브러리 불러오기   
```python
# Pandas는 Numpy 기반으로 만들어졌다.

import pandas as pd
import numpy as np
```

### 1.2 원본 데이터 불러오기
```python
# df = pd.read_확장자('파일명')

df = pd.read_excel('ooo.xlsx')   
df = pd.read_csv('ooo.csv', encoding='utf-8')  

# 한글이 깨지거나 오류가 생기면 하기의 방법으로 해결 시도
# utf-8로 해결이 안되면, cp949 / euc-kr로 시도
with open('ooo.xlsx', mode="r", encoding="utf-8") as file:  
    df = pd.read_excel(file)

```

### 1.3 원본 데이터 선택적 불러오기
```python
# 자료를 읽기 시작할 행(header) 지정
# 읽어올 엑셀의 컬럼(usecoles) 지정

df = pd.read_excel('ooo.xlsx', header=2, usecols="oo, xx") 
```

---

## 2. pandas의 데이터 타입

| 시리즈 | 구성요소 |
| :--: | :-- |
| Series | index, value |
| DataFarame | index, value, column |

### 2.1 Series
- 공식문서 [(링크)](https://pandas.pydata.org/docs/reference/api/pandas.Series.html)  
- index와 value로 이루어져있다.   
- 한 가지 데이터 타입만 가질 수 있다.   
- Parameter   
  - data : array-like, Iterable, dict, or scalar value   
  - dtype : str, numpy.dtype, or ExtensionDtype, optional   


#### 2.1.1 dtype
```python
# dtype : int
- pd.Series([1, 2, 3, 4])                     # dtype : int64
- pd.Series([1, 2, 3, 4], dtype=int)          # dtype : int32
- pd.Series([1, 2, 3, 4], dtype=np.int)       # dtype : int32
- pd.Series([1, 2, 3, 4], dtype=np.int64)     # dtype : int64

# dtype : float
- pd.Series([1, 2, 3, 4], dtype=np.float)     # dtype : float64
- pd.Series([1, 2, 3, 4], dtype=np.float64)   # dtype : float64
- pd.Series([1, 2, 3, 4], dtype=np.float32)   # dtype : float32

# dtype : object
- pd.Series([1, 2, 3, 4], dtype=str)  # dtype : object
```

#### 2.1.2 data
```python
- pd.Series([1,2,3])               # dtype : int64
- pd.Series(np.array([1, 2, 3]))   # dtype : int32
- pd.Series({'key':'value'})       # dtype : object
- pd.Series([1, 2, 3, 4,'5'])      # dtype : object
```


#### 2.1.3 연산
- 데이터 중 연산이 str이 포함되어 있어, 오류 발생
```python
data = pd.Series([1, 2, 3, 4,'5'])
data % 2
```
- 숫자만 있을 경우 연산 가능
```python
data = pd.Series([1, 2, 3, 4])
data % 2
```
0    1   
1    0   
2    1   
3    0   
dtype: int64   

### 2.2 DataFrame()
- 시리즈의 집합
- pd.DataFrame(data, index=oo, columns=xx)
```python
# 예로들어, 난수로 이루어진 행렬(6x4)를 데이터로 하고 
data = np.random.randn(6, 4)

# 2022년 1월 1일부터, 6일간의 기간을 인덱스로 하고
dates = pd.date_range("20220526", periods=6)

# 열 이름을 A,B,C,D로 같는 데이터 프레임을 만들어보자.
df = pd.DataFrame(data, index=dates, columns=['A','B','C','D'])
```

#### 2.1.4 연산
- 시리즈와 마찬가지로 value의 dtype이 숫자여야 함
```
# df의 열A를 열B로 나누는 두가지 방법
1. df['A/B_1'] = df['A']/df['B']
2. df['A/B_2'] = df['A'].div(df['B'], axis=0)
```

---

## 3. 데이터 전처리 방향 설정

> _데이터를 확인 이후 어떤 식으로 데이터를 전처리할 지 방향을 설정해놓고 시작하는 것을 권장_   

### 2.1 데이터 프레임이 완성된 이후 확인해야할 4가지

- 상단 n개의 행 읽기 : df.head()   
- 하단 n개의 행 읽기 : df.tail()   
- 각 열의 기술 통계량 : df.describe()   
- 정보 확인하기 : df.info


### 2.2 인덱스, 컬럼 이름 확인
- 인덱스 이름 : df.index   
- 컬럼 이름 : df.columns


### 2.3 결측치(missing data)를 다루는 대표적인 방법  
- 랜덤하게 채워넣기   
- 주변 행들의 값들로 채워넣기   
- 열의 대푯값을 계산해서 채워넣기 (mean, median 중위값)  
- 전체 행들을 그룹으로 묶어낸 후, 그룹 내 해당 열의 대푯값으로 채워넣기   
- 나머지 열들로 머신러닝 예측모델을 만든 후 해당 열의 값을 예측해 채워넣기      
- 특정 기준 비율 이상으로 빠져있을 시 해당 열 삭제   

```python
df['열이름'].fillna(100)
df['열이름'].dropna()
```

### 2.4 대푯값
- 평균(mean)
- 중위값(median)
- 최빈값(mode)  
- 분산(variance)
- 표준편차 (standard deviation)

---
## 3. 데이터 전처리

### 3.1 데이터 선택하기
#### 3.1.1 열 선택하기
- df[열이름] : 시리즈로 출력
- df.열이름 : 컬럼 이름이 모두 숫자가 아닌 경우 .(점)으로 선택할 수 있음
- df[[열이름]] : 데이터프레임으로 출력
- df[[열이름1, 열이름2, 열이름3,...]] : 데이터프레임에서는 여러 개의 열을 꺼낼 수 있다
- df[열이름].unique() : 해당 컬럼의 중복을 제외한 이름들
- len(df[열이름].unique()) : 해당 컬럼의 중복을 제외한 이름들의 갯수

#### 3.1.2 행 선택하기
- df.loc[행이름] : 시리즈로 출력
- df.loc[[행이름]] : 데이터프레임으로 출력
- df.loc[[행이름1, 행이름2 , 행이름3,...]] : 데이터프레임에서는 여러 개의 행을 꺼낼 수 있다

#### 3.1.3 offset index으로 선택
- [n:m] : n부터 m-1 까지
- 인덱스나 컬럼의 이름으로 slice 하는 경우는 끝을 포함한다

##### 3.1.3.1 `df[:]`
- df[:] : 데이터프레임 전체
- df[0:3] : 행 0부터 2까지
- df["20220101":"20220104"] : 행 1월1일부터 1월4일까지

##### 3.1.3.2 `df.loc[]`
```python
- df.loc[:,:]                                # 행열 전체
- df.loc['20220103':'20220106', 'B':'D']     # 행 3일~6일까지, 열 B부터 D까지   
- df.loc['20220103':'20220106', ['B','D']]   # 행 3일~6일까지, 열 B와 D
- df.loc[['20220103','20220106'], 'B':'D']   # 행 3일과 6일, 열 B부터 D까지
- df.loc[['20220103','20220106'], ['B','D']] # 행 3일과 6일, 열 B와 D
- df.loc['20220103', 'C']                    # 행 1월3일, 열 C
```

#### 3.1.4 특정 위치의 값 선택하기 `df.at[]`
```python
# df.loc['행이름', '열이름']의 결과와 같음
- df.at['행이름', '열이름']
```


#### 3.1.5 인덱스 번호로 선택하기 `df.iloc[]`
- iter location
```python
- df.iloc[3]         # 인덱스 번호 기준 3번째 행
- df.iloc[3,1]       # 인덱스 번호 기준 3번째 행, 1번째 열
- df.iloc[0:3, 0:3]  # 인덱스 번호 기준 0~2번째 행, 0~2번째 열
- df.iloc[2,[0,2]]   # 인덱스 번호 기준 2번째 행, 0번째/2번째 열
- df.iloc[:,[0,2]]   # 인덱스 번호 기준 전체 행, 0번째/2번째 열
- df.iloc[[0,2], 2]  # 인덱스 번호 기준 0번째/2번째 행, 2번째 열
- df.iloc[[0,2], :]  # 인덱스 번호 기준 0번째/2번째 행, 전체 열
```
---

### 3.2 정렬
#### 3.2.1 오름차순 정렬하기
```python
# 내용(value)을 기준으로 정렬(sort), inplace=True : 덮어쓰기
df.sort_values(by='열이름', inplace=True)
```

#### 3.2.2 내림차순 정렬하기
```python
df.sort_values(by='열이름', ascending=False, inplace=True)
```

#### 3.2.3 데이터 기준열 정렬 `set_index()`
- 파일을 불러올 때, 기준열로 정렬하는 방법
```python
# df = pd.read_확장자('파일명')
ⓛ df_2 = pd.read_csv('ooo', encoding='utf-8', index_col='합칠 기준 열 이름')   
② df_2 = pd.read_csv('ooo.csv', encoding='utf-8').set_index('합칠 기준 열 이름')   
```

- 데이터 프레임을 기준열로 정렬하는 방법
```python
# 선택한 컬럼을 데이터프레임의 인덱스로 지정
# inplace : 덮어쓰기 여부
df.set_index('기준 열의 이름', inplace=True)

# 기존 데이터로 원상복구
df.reset_index(inlace=True)
```

---

### 3.3 Condition : 마스킹, 필터링
- 조건
```python
df['A'] > 0           # 칼럼 A의 values 중 양수인 것들 (boolean)
df[['A','B']] > 0     # 칼럼 A,B values 중 양수인 것들 (boolean)
```
- 마스킹 (with 조건)
```python
# 마스킹을 해서 조건에 해당하면 값이 나오고, 아니면 NaN(Not a Number)로 나온다
df[ df[['A','B']] > 0 ]  # df 중 대괄호 안의 조건을 만족하는 values
df[ df>0 ]
```

- isin() : 특정 요소가 있는지 확인 (boolean)
```python
# E열에 'two'와 'seven'이 있는지 boolan으로 반환
df['E'].isin(['two','seven'])

# 해당 조건으로 마스킹을 적용할 수 있음
df[df['E'].isin(["two", "seven"])]
```

- str.contains() : 선택한 열의 문자열에 특정 문자열이 포함되어있는지를 체크
```python
# 요소 한 가지만 확인 가능 (boolean)
df['E'].str.contains('one')

# one을 요소로 하는 것의 행의 갯수 (true=1, false=0)
sum(df['E'].str.contains('one'))

# 필터링 :  one을 요소로 하는 것의 행으로, 열은 전체
df.loc[df['E'].str.contains('one'), :]
```
---

### 3.4 칼럼 만들기
#### 3.4.1 새로운 열 추가
```python
# 기존 칼럼이 없으면 추가
# 기존 칼럼이 있으면 수정

df['E'] = ['one', 'one', 'two', 'three', 'four', 'seven']
df
```

#### 3.4.2 NaN 값으로 새로운 열 채우기
```python
df['A'] = np.nan
```

#### 3.4.3 `apply`
- `apply` : 기존의 열에 기존 열에 함수를 적용해서 새로운 열을 만들때 사용   
- df['새로운 열의 이름'] = df['활용할 기존 열의 이름'].apply(적용할 함수)
```
- df['A'].apply('sum')
- df['A'].apply('mean')
- df['A'].apply('std')
- df['A'].apply('min')
- df['A'].apply('max')
- df['A'].apply(np.sum)
- df['A'].apply(np.mean)
- df['A'].apply(np.std)
- df['A'].apply(np.min)
- df['A'].apply(np.max)
```
- 함수 만들어서 적용시킬 수 있음
```python
def plusminus(num):
    return "plus" if num>0  else "minus"

df['A'].apply(plusminus)
```

- 람다를 사용하면 위의 코드를 한줄로 표현할 수 있음
```
df["A"].apply(lambda num: "plus" if num > 0 else "minus")
```

- 여러 열을 동시에 함수 적용시킬 수 있음
```python
df[['A','D']].apply('sum')
```

#### 3.4.4 A의 데이터프레임을, B의 열 데이터프레임으로 나눌 때
```python
# case 1
df['새로 만들 열이름'] = 데이터프레임A['열이름']/데이터프레임B['열이름']

# case 2
A.div(B['열 이름'], axix=0)

- axis = 0 : 기본적으로 열방향으로 연산 (많은 함수에서 Default)
- axis = 1 : 행방향으로 연산
```



---

### 3.5 변경

#### 3.5.1 행열 이름 조회
- df.columns : 열 이름들의 리스트   
- df.index : 행 이름들의 리스트

#### 3.5.2 열 이름 변경
- df.colums : 열 이름들의 리스트   
- df.index : 행 이름들의 리스트 == 인덱스 열   

```python
# inplace 옵션 == 덮어쓰기 여부
df.rename(columns={'before_1':'after_1'}, index={'before_2':'after_2'}, inplace=True)

# 인덱스명을 바꾸고 싶을때({})
df= df.rename({df.index[0]:'2020', df.index[1]:'2021', df.index[2]:'2022'},axis='index')
```

#### 3.5.6 열의 value의 이름을 변경하고 싶을 때
```python
df['열이름'] = df['열이름'].replace([value_a, value_b], ['1', '2'])
```

#### 3.5.7 열의 순서를 는 방법
- df = df[['d','c','a','b']]
---

### 3.6 삭제하기

#### 3.6.2 `del` : 열 삭제
```python
del df[열이름]
```

#### 3.6.1 `drop` : 행, 열 모두 삭제 가능
- axis parameter (0=가로, 1=세로)
- inplace : 덮어쓰기 
```python
# 열 삭제
df.drop(['D', axis=1])

# 행 삭제
** axis parameter 값을 조정하면 열도 삭제 가능
df.drop([0])
```

---

### 3.7 복사
#### 3.7.1 얕은 복사
```python
# shallow copy  
df_2 = df
```
원본 DataFrame인 df_2와 연결되어 있어, df_2의 변경 내역이 df에도 영향을 미침

#### 3.7.2 깊은 복사
```python
#deep copy  
df_3 = df.copy()
```

원본 DataFrame인 df로부터 분리되어 별도로 존재함   
df_3의 변경 내역이 df에 영향을 미치지 않음

---


### 3.8 이상치 처리

#### 3.8.1 빈 행이 너무 많을 경우 `isnull()`, `notnull()`
```python
# 데이터 개요를 확인했을 때
# Range index에 비해 데이터가 현저히 적을 경우
df.info()

# 해당 열의 데이터를 확인하고
df[열이름].unique

# isnull 메소드로 null 값을 확인하고(boolean)
[df[열이름].isnull()

# 마스킹을 씌워 해당 null만 가져올 수 있다.
df[df[열이름].isnull()].head()

# 반대로 null이 아닌 값만 가져와서 사용할 수 있다.
df = df[df[열이름].notnull()]
```

#### 3.8.2 백분율이 100%가 넘는 경우
```python
# solution 1.
- 이상치를 찾기 위해 : for문과 iterrow, serires를 활용한다
- but. 너무 복잡함

# solution 2.
Masking 기법(체 활용)
- boolean 체크 후 값 대입 적용이 가능
- df[df[['열a','열b','열c', ...]] > 100] = 100
- 복잡하면 안에 있는 데이터 부터

# solution 3.
- DataFrame에서의 필터링
- 판단의 기준은 열로 두고, 필터링의 결과는 전체 행

(1) A가 100 이상일 때 
df[df['열 이름 A'] > 100]]

(2) A가 100 이상이고, B가 100 이상일 때
df[(df['열 이름 A'] > 100) & (df['열 이름 B'] > 100)]]

(2) A가 100 이상이거나, B가 100 이상일 때
df[(df['열 이름 A'] > 100) | (df['열 이름 B'] > 100)]]

(4) A가 100 이상이 아닐 때
df[~(df['열 이름 A'] > 100)]
```

#### 3.8.3 결측치가 있을 경우
```python
df['열이름'].fillna(100)
df['열이름'].dropna()

# 결측치가 채워진 열을 기존 열에 덮어써줘야 하는 것에 유의
# df['열 이름 A'] = df['열 이름 A'].fillna(100)
```


---
### 3.9 데이터 merge

#### 3.9.1 두 가지 서로 다른 데이터를 합치는 세가지 방법
① pd.merge(left, right, how='inner' , on='기준 열 이름')   
- inner : 교집합
- left : 왼쪽 데이터 기준
- right : 오른족 데이터 기준
- outer : 합집합
![image](https://user-images.githubusercontent.com/101171109/170246105-0b4d9924-ac26-4c07-aa79-2c95bbc60e01.png)

  
② A.join(B)   
- merge와 달리, A와 B 기준열의 순서가 맞지 않아도 매칭이 됨    
- 단, A와 B 데이터프레임의 index열의 길이가 동일해야 함  

③ pd.concat([A, B], axix=?) # concatenate   
- 그대로 이어붙이는 방법   
- axis = 0 : 기본적으로 열방향으로 연산 (많은 함수에서 Default)   
- aixs = 1 : 행방향으로 연산   



---




### 3.10 열의 중복되는 데이터를 처리하며 기준열을 만들때 : `pivot_table`  
- 피벗테이블 기본 형태 : index, columns, values, aggfunc
```python
# 기준열로 정렬되며, 숫자데이터가 aggfunc으로 처리된다.
pivot_df = pd.pivot_table(df, index='기준 열 이름', aggfunc=np.mean)

# Aggregation function == 집계 함수
# np.mean, np.max, np.min, len ... (평균이 기본 설정값)
```

- index, columns, value, aggfunc를 여러개 넣어 사용 가능하다
```
df.pivot_table(
    index=["A", "B", "C"],
    columns=["a", "b"],
    values=["1", "2"], 
    aggfunc=[np.sum, np.mean],
    fill_value=0, # NaN 0으로 처리
    margins=True) # 총계(All) 추가
```

- 다중 컬럼(Multi column) 조회 방법
```python
pivot_df['level0 컬럼','level1 컬럼','level2 컬럼', ...]
```

- 다중 컬럼(Multi column) 제거 방법
```python
# 특정 레벨의 컬럼을 제거할 수 있다
pivot_df.columns = pivot_df.columns.droplevel([0,1])
```

---
### 3.11 Pandas 반복문용 명령 `iterrows()`
- Pandas 데이터 프레임은 대부분 2차원이다    
- Pandas 데이터 프레임으로 반복문을 만들때 itterows() 옵션을 사용하면 편하다    
- 사용시 인덱스와 내용으로 나누어 받을 수 있다
```python
for idx, rows in df.iterrows():
  print(idx) # 인덱스
  print(rows) # 내용
```
---

## 4. 통계
### 4.1 상관계수
- df.corr()
- correlation의 약자
