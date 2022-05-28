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

## 1. matplotlib 기초
- [공식문서](https://matplotlib.org/stable/gallery/index)

### 1.1 라이브러리 불러오기
```python
# import matplotlib as mpl
# matplotlib에서 pyplot 기능을 plt라는 이름으로 가져와서 사용
import matplotlib.pplot as plt

# 한글설정
from matplotlib import rc
rc("font", family="Malgun Gothic")

# 마이너스 부호 때문에 한글이 깨질 수가 있어 주는 설정
#plt.rcParams["axes.unicode_minus"]로 대체 가능
rc('axes', unicode_minus=False)

# 주피터 노트북에서 그래프를 그릴 수 있도록 하는 설정
# %matplotlib inline로 대체 가능 
get_ipython().run_line_magic("matplotlib", "inline")
```

### 1.2 그래프 그리기
#### 1.2.1 그래프 그리기 기본 형태
- plt.figure(figsize=(10, 6)) : 도화지 사이즈    
- plt.plot(x, y) : x축과 y축 데이터 할당   
- plt.show : 그리기   

#### 1.2.2 그래프 그리기 기초 예제
##### 1.2.2.1 삼각함수
- np.arange(a, b, s): a부터 b까지 s의 간격   
- np.sin(value)   
- np.cos(value)
```python
# 삼각함수 계산을 위해 numpy 임포트
import numpy as np 

# x축, y축 할당
x = np.arange(0, 10, 0.01)
y = np.sin(x)

# 도화지를 펼치고
plt.figure(figsize=(10, 6))

# 그림을 그리고
plt.plot(x, np.sin(x))
plt.plot(x, np.cos(x))

# 시각화 확인
plt.show()
```
- 디테일 설정
```python
def drawGraph():
    # 도화지를 펼치고
    plt.figure(figsize=(10, 6))
    
    # 그림을 그리고
    plt.plot(x, np.sin(x), label="sin")
    plt.plot(x, np.cos(x), label="cos")
    
    # 디테일을 설정하고
    plt.grid(True) # 격자무늬 
    plt.legend(loc='upper right') # 범례(위치)
    plt.title("Sample") # 제목
    plt.xlabel("time") # x축 제목
    plt.ylabel("Amplitude") # y축 제목 
    
    # 시각화 확인
    plt.show()
    
drawGraph()
```
#### 1.2.2.2 그래프 커스텀
- 마커 색상, 모양
```python
x = np.arange(0, 5, 0.5)

# 도화지를 펼치고
plt.figure(figsize=(10, 6))

# 그림을 그리고
plt.plot(x, x, "r--") # red ---- 
plt.plot(x, x ** 2, "bs") # blue square
plt.plot(x, x ** 3, "g>") # green >

# 디테일 설정하고
plt.grid(True)

# 시각화 확인
plt.show()
```

- 라인/마커 색상, 모양
```python
x = list(range(0, 7))
y = [1, 4, 5, 8, 9, 5, 3]

def drawGraph():
    # 도화지 펼치기
    plt.figure(figsize=(10, 6))
    
    # 그림 그리기
    plt.plot(
        x,
        y,
        # 라인
        color="red", 
        linestyle="--", #'dashed','-'
        
        # 마커
        marker="o", 
        markerfacecolor="blue",
        markersize=10, 
    )

    # 디테일 설정
    plt.grid(True)
    
    # x축과, y축의 범위 지정
    plt.xlim([-0.5, 6.5]) 
    plt.ylim([0.5, 9.5])
    plt.show() 
    
drawGraph()
```

#### 1.2.2.3 산점도(scatter plot)
- 산점도 기본 형태
```python
x = np.array(range(0, 10))
y = np.array([9, 8, 7, 9, 8, 3, 2, 4, 3, 4])

def drawGraph():
    # 도화지 펼치기
    plt.figure(figsize=(10, 6))
    # 그림 그리기
    plt.scatter(x, y)
    # 디테일 설정
    plt.grid(True)
    # 시각화 확인
    plt.show()
    
drawGraph()
```
- 산점도 커스텀
```python
x = np.array(range(0, 10))
y = np.array([9, 8, 7, 9, 8, 3, 2, 4, 3, 4])

colormap = x 

def drawGraph():
    # 도화지 펼치기
    plt.figure(figsize=(10, 6))
    
    # 그림 그리기
    # s=마커의 크기, c=색상을 칠할 데이터, marker= 마커 모양
    plt.scatter(x, y, s=150, c=colormap, marker="<")
    # 색상바 생성
    plt.colorbar()
    plt.show()
    
drawGraph()
```

#### 1.2.2.4 Pandas에서 plot 그리기
- matplotlib으로 데이터프레임에서 바로 그래프를 그릴 수 있다. 
- 일반적으로 데이터가 많은 경우 정렬 후 그리는 것이 효과이다.   
```python
# 막대그래프
df["A"].plot(kind="bar", figsize=(5, 5))

# 막대그래프(가로방향)
df["A"].plot(kind="barh", figsize=(5, 5))
```

___

## 2. 열지도로 데이터 시각화 하기
### 2.1 라이브러리 불러오기
```python
import seaborn as sns
import matplotlib.pyplot as plt


# 한글 깨짐 방지
from matplotlib import font_manager
%matplotlib inline   

font_name = font_manager.FontProperties(fname="c:/Windows/Fonts/malgun.ttf").get_name()  
rc('font', family=font_name)
```

### 2.2 matplotlib으로 도화지 깔기
```python
plt.figure(figsize = (10, 10), dpi = 100)
```

### 2.3 seaborn으로 그래프 올려놓기**
```python
sns.heatmap(df (by='정렬기준', ascending=False), annot=True, fmt='f', linewidths=.5, cmap='Reds' )
```
- df : 그래프로 만들 데이터 프레임
- by : 정렬기준열 이름
- ascending : 정렬 방향
- annot : 셀 내에 수치 입력 여부  
- fmt : 셀 내 입력될 수치의 format (f == float)  
- linewidths : 셀 간 이격거리 (하얀 부분, 내부 테두리)
- 모든 내용을 외울 필요는 없음 (필요할 때마다 찾아서)
- cmap : [https://goo.gl/YWpBES](https://goo.gl/YWpBES)

### 2.4 도화지 이름
```
plt.title('도화지 이름')
```

### 2.5 도화지 출력
```
plt.show()
```

### 2.6 이슈 해결
- 데이터의 색의 차이가 분별이 안 됨 
```python
# 정규화(Feature scaling/ Feature Nomalization)

① Min-Max algorithm : 최댓값을 1, 최솟값을 0으로 맞춰줌
② Standardization (표준화) : 열마다의 평균값이 0, 표준편차가 1로 맞춰줌
③ ...

# 활용
ex. 4개 열의 수치 중 최대값으로 나눠줌   
max_col = df[['a', 'b', 'c', 'd']].max()_
result = df[['a', 'b', 'c', 'd']] / max_col
```

---

## 3. 지도 시각화 : Folium library 활용 / 지도 데이터 : GeoJSON 활용
### 3.1 json 파일 불러오기
```python
import json

geo_path = '파일명.json'
geo_str = json.load(open(geo_path, 'r' , encoding='utf-8'))
```
- load <-> dump : 불러오는 것은 load, 저장하는 것은 dump

### 3.2 json
- Javascript Object Notation   
- 데이터 교환을 위한 표준 포맷   
- XML, YAML는 json 이전의 표준 포맷   

### 3.3 pyptny
- JSON 구조를 쉽게 파악할수 있게 해주는 도구   

#### 3.3.1 pyptny 설치
- !pip install pyprnt==2.3.3

#### 3.3.2 pyptny 임포트
- from pyprnt import prnt

#### 3.3.3 ptptny 활용법
- print(json 자료, truncate=True, width=80)
- truncate : 안에 있는 내용이 너무 길면 잘라줌
- width : 내용이 찌그러질 때 조절

---

## 4. 포리움으로 지도에 그래프 그리기
#### 4.1 포리움 설치
- !pip install folium==0.5.0

#### 4.2 포리움에 맵클래스의 생성자
```python
import folium  
map = folium.Map(location=\[37.5502, 126.982\], zoom\_start=11, tiles='Stamen Toner') 
```
- folium에서 Map이라는 클래스를 사용   
- location : 초기 지도 center 위치 (위도, 경도)    
- zoom start : 줌 크기   
- tiles : 지도 타입 (default type or "Stamen Terrain" or "Stamen Toner"   

---
## 5. Choropleth map : 행정구역별로 색칠해놓은 지도
```python
import json

geo_path = '파일명.json'
geo_str = json.load(open(geo_path, 'r' , encoding='utf-8'))

map.choropleth(geo_data = geo_str, # 가져온 JSON 파일
                     data = df['열이름'], # 시각화의 대상이 될 데이터
                     columns = [df['열이름1'], df['열이름2']] # 가져올 열이 인덱스 열일 때 -> df.index 
                     fill_color = 'PuRd' #color brewer([http://colorbrewer2.org/](http://colorbrewer2.org/))
                     key_on = 'feature.id'  # GeoJSON 규약을 따름
```
---

## 6. CircleMarker

#### 6.1 구글 클라우드 플랫폼 API
```
!pip install googlemaps==4.6.0

import googlemaps  
gmaps = googlemaps.Client(key="personal\_key")

tmpMap = gmaps.geocode('보라매공원', language="ko")  
tmpMap
```

#### 6.2 포리움에 맵클래스의 생성자
```
map = folium.Map(location=[37.5502, 126.982], zoom_start=11)
```

#### 6.3 CircleMarker
```python
for n in df.index:
    folium.CircleMarker(위도, 경도, radius=? , color='#3186cc', fill=True, fill\_color='#3186cc').add\_to(map)

- radius가 자동으로 meter 단위가 된다.
- radius=value\*0.5, # circle 의 크기를 결정
- color='#3186cc', fill=True, fill\_color='#3186cc' : #16진수 컬러
- ↑ 테두리색, 내부색여부, 내부색
```
---

## 7. 결과값 다른 확장자 파일로 저장
### 7.1 DF to csv file  
- df.to\_csv('processed\_data.csv', encoding='utf-8')

### 7.2 saving a folium map as an HTML file
- map.save('folium\_map.html')

---
## 8. 기타
- `startswith()`, `endswith()`
```python
'python'.startswith('py') -> True
'python'.endswith('on') -> True
```
---

## 9. 단어 등장 빈도 시각화
```python
import nltk
import matplotlib
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc

font_name = matplotlib.font_manager.FontProperties(fname="C:/Windows/Fonts/malgun.ttf").get_name() # NanumGothic.otf
matplotlib.rc('font', family=font_name)

word_counted = nltk.Text(word_cleaned) 
plt.figure(figsize=(15, 7)) # plot 영역(그래프 영역)의 크기를 지정합니다.
word_counted.plot(50) # "plot" the graph, 상위 50개 단어를 보여줍니다.
```

## 10. 단어 등장 빈도 시각화 (막대그래프)

```
# 막대그래프로의 시각화는 NLTK 의 함수만으로 진행하기 어려우므로,
# NLTK의 FreqDist 함수를 적용한 후 Pandas의 Dataframe에 데이터를 담은 다음 시각화를 진행합니다.

word_frequency = nltk.FreqDist(word_cleaned) # Frequency Distribution
word_frequency

# 단어 빈도가 담긴 Dict 로부터 값을 가져와 DataFrame 을 만듭니다.
df = pd.DataFrame(list(word_frequency.values()), word_frequency.keys()) 

# 빈도 내림차순으로 정렬합니다.
result = df.sort_values([0], ascending=False)

# 전체 데이터(단어 수)는 너무 많기 때문에 출현 횟수 상위 50개만 가져와 시각화합니다.
result = result[:50]
# result


# 데이터프레임에 담긴 단어 및 빈도 수를 막대그래프로 표현하기 위한 코드입니다.

result.plot(kind='bar', legend=False, figsize=(15,5)) # 'bar' graph
# 그림 사이즈를 변경하고 싶을 경우 figsize=(가로, 세로) 를 변경합니다.
# 기타 그래프 관련 옵션은 https://goo.gl/YNejGt 에서 확인하고 적용하실 수 있습니다.

plt.show()
```

---

## 11. 워드 클라우드
```python
# 라이브러리 임포트
from wordcloud import WordCloud
import matplotlib.pyplot as plt
from PIL import Image

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline


# 워드 클라우드 도화지 깔고
word_cloud = WordCloud(font_path="C:/Windows/Fonts/malgun.ttf",
                       width=2000, height=1000, # 이 부분을 수정하시면 실제 워드클라우드의 크기가 바뀝니다 (해상도가 바뀝니다)
                       # prefer_horizontal= 1.0, # 이 부분의 주석을 해제하시면 단어들이 가로로만 그려지게 됩니다. (0~1)
                       background_color='white')
                       

# 도화지 위에 그림 그리기
word_cloud.generate_from_frequencies(word_dic)


plt.figure(figsize=(15,15))
plt.imshow(word_cloud) # image show
plt.axis("off")
plt.tight_layout(pad=0)
plt.show()
```

## 12. 특정 그림 테두리 내에 워드 클라우드 그리기
```python
from PIL import Image
from wordcloud import ImageColorGenerator # Image 로부터 Color 를 생성(Generate)해내는 객체입니다.

# 수치 행렬을 준비
python_coloring = np.array(Image.open("python_mask.jpg"))
image_colors = ImageColorGenerator(python_coloring)

word_cloud = WordCloud(font_path="C:/Windows/Fonts/malgun.ttf",
                       width=2000, height=1000, 
                       mask=python_coloring, # "마스크를 씌운다"라고 표현합니다.
                       background_color='white').generate_from_frequencies(word_dic)

plt.figure(figsize=(15,15))

# plt.imshow는 np.array를 받아 이미지로 보여줌
plt.imshow(word_cloud.recolor(color_func=image_colors), interpolation='bilinear')
# Matplotlib colormap 활용 (http://j.mp/32UXOQ6)
# plt.imshow(word_cloud.recolor(colormap='Blues'), interpolation='bilinear')

plt.axis("off")
plt.tight_layout(pad=0)
plt.show()

# 아래 코드를 실행하시면 jupyter notebook 과 동일한 폴더에 워드클라우드가 이미지 파일로 저장된 것을 확인하실 수 있습니다.
word_cloud.to_file("word_cloud_completed.png") # Save "to file"
```

## 13. 요약
- 워드 클라우드의 해상도는 원본이미지를 넘어설 수 없음
```python
# 아래 옵션들을 원하시는대로 지정하셔서 가장 마음에 드는 워드클라우드를 활용하시면 됩니다.

word_cloud = WordCloud(font_path="C:/Windows/Fonts/malgun.ttf", # 한글 폰트 변경
                       width=2000, height=1000, # 실제 워드클라우드 크기 변경 (해상도 변경)
                       max_words=100, # 최대로 보여질 단어 수 제한
                       background_color='white', # 바탕색 지정 (주석처리할 경우 검정으로 변경됨)
#                      max_font_size=100, # 최대 단어 크기 제한
                      ).generate_from_frequencies(word_dic)

plt.figure(figsize=(15,15)) # Jupyter notebook 상에서 보여지는 워드클라우드 크기 지정 
plt.imshow(word_cloud)
plt.axis("off")
plt.tight_layout(pad=0)
plt.show()

# word_cloud.to_file("word_cloud_7 (white, squared, max100).png")
```
