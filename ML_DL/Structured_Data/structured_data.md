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
import pandas as pd
```

### 1.2 원본 데이터 불러오기
```python
# df = pd.read_확장자('파일명')

df = pd.read_excel('ooo.xlsx')   
df = pd.read_csv('ooo.csv', encoding='utf-8')  

# 한글이 깨지거나 오류가 생기면 하기의 방법으로 해결 시도
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

## 2. 데이터 전처리 방향 설정

> _데이터를 확인 이후 어떤 식으로 데이터를 전처리할 지 방향을 설정해놓고 시작하는 것을 권장_   

### 2.1 데이터 프레임이 완성된 이후 확인해야할 4가지

- 상단 n개의 행 읽기 : df.head()   
- 하단 n개의 행 읽기 : df.tail()   
- 각 열의 기술 통계량 : df.describe()   
- 정보 확인하기 : df.info


### 2.2 결측치(missing data)를 다루는 대표적인 방법  
- 랜덤하게 채워넣기   
- 주변 행들의 값들로 채워넣기   
- 열의 대푯값을 계산해서 채워넣기 (mean, median중윗값)  
- 전체 행들을 그룹으로 묶어낸 후, 그룹 내 해당 열의 대푯값으로 채워넣기   
- 나머지 열들로 머신러닝 예측모델을 만든 후 해당 열의 값을 예측해 채워넣기      
- 특정 기준 비율 이상으로 빠져있을 시 해당 열 삭제   

```python
df['열이름'].fillna(100)
df['열이름'].dropna()
```

### 2.3 대푯값
- 평균(mean)
- 중위값(median)
- 최빈값(mode)  
- 분산(variance)
- 표준편차 (standard deviation)

---

## 3. 데이터 전처리

### 3.1 pandas의 데이터 타입
- pandas.DataFrame() : 시리즈의 묶음  
- pandas.Series() : 각각의 행과 열, Key 값이 있는 list

### 3.2 선택하기
#### 3.2.1 행 선택하기
- df.loc[a] : 시리즈로 출력
- df.loc[[a]] : 데이터프레임으로 출력
- df.loc[[a,b,c,...]] : 데이터프레임에서는 여러 개의 행을 꺼낼 수 있다

#### 3.2.2 열 선택하기
- df[a] : 시리즈로 출력
- df.a : 컬럼 이름이 모두 숫자가 아닌 경우 .(점)으로 선택할 수 있음
- df[[a]] : 데이터프레임으로 출력
- df[[a,b,c,...]] : 데이터프레임에서는 여러 개의 열을 꺼낼 수 있다

#### 3.2.4 offset index으로 선택
- [n:m] : n부터 m-1 까지
- 인덱스나 컬럼의 이름으로 slice 하는 경우는 끝을 포함한다
```python
- df.loc['3', 'c']             # 행 3과, 열 c
- df.loc['3':'6', 'a':'c']     # 행 3부터 6까지, 열 a부터 c까지   
- df.loc['3':'6', ['a','c']]   # 행 3부터 6까지, 열 a와 c
- df.loc[['3','6'], 'a':'c']   # 행 3과 6, 열 a부터 c까지
- df.loc[['3','6'], ['a','c']] # 행 3과 6, 열 a와 c
 ```

#### 3.2.3 인덱스 번호로 선택
- iter location
```python
- df.iloc[3]
- df.iloc[3,1]
- df.iloc[0:3, 0:3]
- df.iloc[2,[0,2]]
- df.iloc[:,[0,2]]
 ```

#### 3.2.5 특정 위치의 값을 출력
- df.at['행이름', '열이름']
---

### 3.3 만들기

#### 3.3.1 기존 열에 함수를 적용해서 새로운 열을 만들때 : `apply`
```
df ['새로운 열의 이름'] = df['활용할 기존 열의 이름'].apply(적용할 함수)
** 람다 개념정리 필요!
```

#### 3.3.2 열의 중복되는 데이터를 처리하며 기준열을 만들때 : `pivot_table`  
```python
pivot_df = pd.pivot_table(df, index='기준 열 이름', aggfunc=np.sum)

# Aggregation function == 집계 함수
# np.mean, np.max, np.min, ...
# 기준열과 일대일 매칭이 되지 않을때 사용
```

#### 3.3.3 열에 중복되는 데이터가 없어 기준열만 설정할 때
```python
df.set_index('기준 열의 이름', inplace=True)

# 기존 데이터로 원상복구
df.reset\_index(inlace=True)
```

#### 3.3.4 A의 데이터프레임을, B의 열 데이터프레임으로 나눌 때
```python
# case 1
df['새로 만들 열이름'] = 데이터프레임A['열이름']/데이터프레임B['열이름']

# case 2
A.div(B['열 이름'], axix=0)

- axis = 0 : 기본적으로 열방향으로 연산 (많은 함수에서 Default)
- axis = 1 : 행방향으로 연산
```

#### 3.3.5 열의 value의 이름을 바꾸고 싶을 때
```python
df['열이름'] = df['열이름'].replace([value_a, value_b], ['1', '2'])
```

#### 3.3.6 특정한 열에서 등장했던 value의 빈도
```python
df['열이름'].value_counts() -> serires 
```

#### 3.3.7 시리즈로 데이터 시각화하기
```python
df['열이름'].value_counts().plot(kind = 'pie')
```

#### 3.3.8 데이터프레임 만들기 예시**
```python
crosstab = pd.crosstab(df.propensity, df.skin, margins=True)  
  
crosstab.columns=\["건성", "민감성", "중성", "지성", "여드름성", "합계"\]  
crosstab.index=\["비교적 저렴한 제품", "중간정도의 제품", "비교적고가의 제품", "합계"\]  
crosstab
```
---

### 3.4 삭제하기

#### 3.4.1 행 삭제하기
```python
df.drop(['a','b','c', ...])
안에 있는 이름 여러 개 지울 수 있다
** axis parameter 값을 조정하면 열도 삭제 가능
```

#### 3.4.2 열 삭제하기
```python
del df[열이름]
```
---

### 3.5 바꾸기

#### 3.5.1 행열 이름 조회
- df.columns : 열 이름들의 리스트   
- df.index : 행 이름들의 리스트

#### 3.5.2 열 이름 바꾸기
- df.colums : 열 이름들의 리스트   
- df.index : 행 이름들의 리스트 == 인덱스 열   

```python
# inplace 옵션 == 덮어쓰기 여부
df.rename(columns={'before_1':'after_1', 'before_1':'after_2'}, inplace=True) 
```
---

### 3.6 정렬
#### 3.6.1 오름차순 정렬하기
```python
# 내용(value)을 기준으로 정렬(sort), inplace=True : 덮어쓰기

df.sort_values(by='열이름', inplace=True)
```

#### 3.6.2 내림차순 정렬하기
```python
df.sort_values(by='열이름', ascending=False, inplace=True)
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

#### 3.8.1 백분율이 100%가 넘는 경우
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

#### 3.8.2 결측치가 있을 경우
```python
df['열이름'].fillna(100)
df['열이름'].dropna()

# 결측치가 채워진 열을 기존 열에 덮어써줘야 하는 것에 유의
# df['열 이름 A'] = df['열 이름 A'].fillna(100)
```

___
### 3.9 조회

#### 3.9.1 선택한 열의 문자열에 특정 문자열이 포함되어있는지를 체크
```python
# true -> 1 / false ->0

df["여행지"].str.contains('계곡')
sum(df["여행지"].str.contains('계곡'))
```


#### 3.9.2 선택한 열의 문자열에 특정 문자열이 포함된 열들만 선택하고자 할 경우(필터링)
```python
df.loc[df['여행지'].str.contains('계곡'), :]
```

### 3.9.3 범위로 지정해 꺼내기 & 열까지 범위 지정하기
```python
df.loc[[3:6, 'a':'b']]
```
뒤까지 모두 포함하는 범위임을 유의   
인덱스가 아니라 이름

---
### 3.10 데이터 merge

#### 3.10.1 데이터 불러오기 : df = pd.read_확장자('파일명')

ⓛ df\_2 = pd.read\_csv('merge\_file.csv', encoding='utf-8', index\_col='합칠 기준 열 이름')   
② df\_2 = pd.read\_csv('merge\_file.csv', encoding='utf-8').set\_index(합칠 기준 열 이름)   

- csv 파일이 한글이 깨지면 인코딩 입력   
- 위의 두 가지의 결과는 같음

#### 3.10.2 두 가지 서로 다른 데이터를 합치는 세가지 방법
① A. join(B)   
- A, B의 기준열 순서가 맞지 않아도 매칭이 됨    
- (조건) 단, A와 B 데이터프레임의 index 열이 동일해야 함    
  

② pd.merge(A, B, left\_on="기준 열 이름 a", right\_on="기준 열 이름 b", how='inner')   
- A, B의 기준열 순서가 맞지 않아도 매칭이 됨   
- inner, left, rightm outer   

![image](https://user-images.githubusercontent.com/101171109/170246105-0b4d9924-ac26-4c07-aa79-2c95bbc60e01.png)

③ pd.concat(\[A, B\], axix=?) # concatenate   
- A, B의 기준열 순서가 맞지 않으면 매칭이 안 됨   
- 그대로 이어붙이는 방법   
- axis = 0 : 기본적으로 열방향으로 연산 (많은 함수에서 Default)   
- aixs = 1 : 행방향으로 연산   

### 3.10.3 열의 순서를 바꾸는 방법
- df = df[['d','c','a','b']]


