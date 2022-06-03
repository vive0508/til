데이터 시각화
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

___

## 1. seaborn 기초

## 1.1 seaborn 설치 및 모듈 임포트
```python
# seaborn이 설치가 안되어있다면 아래의 코드 중 하나로 설치
!conda install -y seaborn 
!pip install seaborn

# seaborn은 matplotlib과 함께 실행된다
import matplotlib.pyplot as plt 
import seaborn as sns 
from matplotlib import rc 

# 한글 설정
plt.rcParams["axes.unicode_minus"] = False 
rc("font", family="Malgun Gothic")

# 주피터 노트북에서 그래프를 그리기 위한 설정
get_ipython().run_line_magic("matplotlib", "inline")

```

---

## 2. seaborn 기본 형태
```python
# 도화지 그리기 (dpi는 옵션)
plt.figure(figsize = (10, 6), dpi = 100)

# 그림 그리기
plt.plot(x, y, x, y2, x, y3)

# 시각화
plt.show()
```

### 2.1 seaborn 기본 형태 + 디테일 설정
- sns.set_style()
```
# style에 white, whitegrid, dark, darkgrid, sticks를 적용할 수 있다.
sns.set_style("white")
plt.figure(figsize=(10, 6))
plt.plot(x, y, x, y2, x, y3)
plt.show()
```
- sns.despine()
```
# despine()으로 왼쪽, 아랫쪽 선만 남겨놓을 수 있다
# offset으로 왼쪽, 아랫쪽 선의 간격을 조정할 수 있다(옵션)
sns.set_style("white")
plt.figure(figsize=(10, 6))
plt.plot(x, y, x, y2, x, y3)
sns.despine(offset=10)
plt.show()
```

---

## 3. seaborn : tips data
```python
# seaborn에서 제공하는 데이터셋이 있음
tips = sns.load_dataset("tips")
```

### 3.1 boxplot
- 기본 형태
```python
# 도화지를 펼치고
plt.figure(figsize=(8, 6))

# 그림을 그리고
sns.boxplot(x=tips["total_bill"])

# 시각화
plt.show()
```
- x값, y값 설정
```python
# 도화지를 펼치고
plt.figure(figsize=(8, 6))

# 그림을 그리고
sns.boxplot(x="day", y="total_bill", data=tips)

# 시각화
plt.show()
```
- hue, palette 옵션
```
# hue : 카테고리 데이터 표현
# palette : 색상 표현 (Set1~Set3)
plt.figure(figsize=(8, 6))
sns.boxplot(x="day", y="total_bill", data=tips, hue="smoker", palette="Set1") 
plt.show()
```

### 3.2 swarmplot
- 기본 형태
```python
plt.figure(figsize=(8, 6))
sns.swarmplot(x="day", y="total_bill", data=tips) 
plt.show()
```
- color 옵션
```python
# color: 0~1 사이 검은색부터 흰색 사이 값을 조절 
plt.figure(figsize=(8, 6))
sns.swarmplot(x="day", y="total_bill", data=tips, color="0.5") 
plt.show()
```
- boxplot with swarmplot
```python
# 도화지를 펼치고
plt.figure(figsize=(8, 6))

# 그림을 그리고
sns.boxplot(x="day", y="total_bill", data=tips)
sns.swarmplot(x="day", y="total_bill", data=tips, color="0.25")

# 시각화
plt.show()
```

### 3.1 lmplot
- 데이터 간의 관계를 파악하고 싶을 때 사용
- 색칠된 데이터의 간격이 좁을수록 강한 상관관계
```python
# height는 size와 관련된 옵션
sns.set_style("darkgrid")
sns.lmplot(x="total_bill", y="tip", data=tips, height=7) 
plt.show()
```
- hue 옵션
```python
sns.set_style("darkgrid")
sns.lmplot(x="total_bill", y="tip", data=tips, height=7, hue="smoker")
plt.show()
```

---

## 4. seaborn : anscombe data
```python
# seaborn에서 제공하는 데이터셋이 있음
anscombe = sns.load_dataset("anscombe")
```

### 4.1 lmplot
```python
# query라는 매서드로 I에 해당하는 데이터셋만 가져옴
# ci 신뢰구간 선택, None 옵션은 신뢰구간 영역 보이는 옵션을 끄는 것
# order : 차수에 따라 옵션 변경 
# robust : 원본에서 많이 떨어진 데이터(outlier)는 없는 셈 친다
# scater_kws 마커사이즈 변경

sns.set_style("darkgrid")
sns.lmplot(
    x="x", 
    y="y", 
    data=anscombe.query("dataset == 'III'"),
    order=1,
    robust=True,  
    ci=None, 
    scatter_kws={"s": 80},
    height=7)
plt.show()
```
---

## 5. seaborn : flight data
```python
# seaborn에서 제공하는 데이터셋이 있음
flights = sns.load_dataset("flights")

# pivot을 사용하여 데이터 정리
flights = flights.pivot(index="month", columns="year", values="passengers")
flights.head()
```

### 5.1 heatmap
- 기본 형태
```python
# annot=True 데이터 값 표시
# fmt="d" 정수형 표현, fmt="f" 실수형 표현
plt.figure(figsize=(10, 8))
sns.heatmap(data=flights, annot=True, fmt="d")
plt.show()
```
- colormap 옵션 [링크](https://goo.gl/YWpBES)
```python
# 색상은 위의 링크에서 확인
plt.figure(figsize=(10, 8))
sns.heatmap(flights, annot=True, fmt="d", cmap="YlGnBu")
plt.show()
```
- 추가 옵션
```python
# df : 그래프로 만들 데이터 프레임
# by : 정렬기준열 이름
# ascending : 정렬 방향
# linewidths : 셀 간 이격거리 (하얀 부분, 내부 테두리)
# 모든 내용을 외울 필요는 없음 (필요할 때마다 찾아서)
sns.heatmap(df (by='정렬기준', ascending=False), annot=True, fmt='f', linewidths=.5, cmap='Reds' )
```

---

## 6. seaborn : iris data
```python
# seaborn에서 제공하는 데이터셋이 있음
iris = sns.load_dataset("iris")
```

### 6.1 pairplot
- 기본 형태
```python
sns.pairplot(iris)
plt.show()
```

- 옵션
```python
# set_style : white, whitegrid, dark, darkgrid,sticks
# hue : 카테고리 데이터 표현
sns.set_style("ticks")
sns.pairplot(iris, hue="species")
plt.show()
```

- 원하는 컬럼만 pairplot
```python
# case 1. x축, y축을 지정하는 방법
sns.pairplot(iris, 
             x_vars=["sepal_width", "sepal_length"], 
             y_vars=["petal_width", "petal_length"])
plt.show()

# case 2.
# kind : scatter', 'kde', 'hist', 'reg'
# reg(regression) : 회귀분석
sns.pairplot(iris, 
             vars=["sepal_width", "sepal_length"],
             kind="reg",
             height=3)
```



