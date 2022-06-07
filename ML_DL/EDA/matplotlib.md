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
# plt.rcParams["axes.unicode_minus"]로 대체 가능
rc('axes', unicode_minus=False)

# 주피터 노트북에서 그래프를 그릴 수 있도록 하는 설정
# %matplotlib inline로 대체 가능 
get_ipython().run_line_magic("matplotlib", "inline")
```


- 플랫폼을 활용한 한글 설정
```python
import platform
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc

get_ipython().run_line_magic("matplotlib", "inline")

# %matplotlib inline
path = "c:/Windows/Fonts/malgun.ttf"

if platform.system() == "Darwin":
    print("Hangul OK in your MAC !!!")
    rc("font", family="AppleGothic")
elif platform.system() == "Windows":
    font_name = font_manager.FontProperties(fname=path).get_name()
    print("Hangul OK in your Windows !!!")
    rc("font", family=font_name)
else:
    print("Unknown system... sorry~~~~")

# plt.rcParams["axes.unicode_minus"]
plt.rcParams["axes.unicode_minus"] = False
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

#### 1.2.2.3 Pandas에서 plot 그리기
- matplotlib으로 데이터프레임에서 바로 그래프를 그릴 수 있다. 
- 일반적으로 데이터가 많은 경우 정렬 후 그리는 것이 효과이다.   
```python
# 막대그래프
df["A"].plot(kind="bar", figsize=(5, 5))

# 막대그래프(가로방향)
df["A"].plot(kind="barh", figsize=(5, 5))
```

#### 1.2.2.4 산점도(scatter plot)
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

#### 1.2.2.5 데이터의 경향 확인
- Numpy를 이용한 1차 직선 만들기(선형회귀)
```python
- np.polyfit(): 직선을 구성하기 위한 계수를 계산
- np.poly1d(): polyfit 으로 찾은 계수로 파이썬에서 사용할 수 있는 함수로 만들어주는 기능 
```
- np.polyfit(x축, y축, 1)
```python
import numpy as np 

fp1 = np.polyfit(df['A'], df['B'], 1)
f1 = np.poly1d(fp1)
```
- 경향선을 그리기 위한 X 데이터 생성 `np.linspace`
```python
# np.linspace(a, b, n): a부터 b까지 n개의 등간격 데이터 생성
fx = np.linspace(100000, 700000, 100)
```
- 경향선과 함께 그래프 그리기
```python
def drawGraph():
    # 도화지를 그린다
    plt.figure(figsize=(10, 6))
    
    # 원래 하던대로 그래프를 그린다
    plt.scatter(df["A"], df["B"], s=50)
    
    # 경향선을 그린다
    # ls=선스타일, lw=선굵기, color=색상
    plt.plot(fx, f1(fx), ls="dashed", lw=3, color="g")
    
    # 디테일 설정
    plt.xlabel("A")
    plt.ylabel("B")
    plt.grid(True)
    
    # 시각화 확인
    plt.show() 

drawGraph()
```

#### 1.2.2.6 강조하고 싶은 데이터 시각화
- 경향(trend)와의 오차를 만든다.
```python

# 경향(trend)
fp1 = np.polyfit(df["A"], df["B"], 1) 
f1 = np.poly1d(fp1) 
fx = np.linspace(100000, 700000, 100) 

# 오차 (실제 y값, 경향에 따르는 x 기댓값)
df["오차"] = df["B"] - f1(df["A"])
```
- 경향과 비교해서 데이터의 오차가 너무 나는 데이터를 계산 
```python
df_sort_f = df.sort_values(by="오차", ascending=False) # 내림차순 
df_sort_t = df.sort_values(by="오차", ascending=True) # 오름차순 
```
- 색상 커스터마이징
```python
from matplotlib.colors import ListedColormap

# colormap 을 사용자 정의(user define)로 세팅 
color_step = ["#e74c3c", "#2ecc71", "#95a9a6", "#2ecc71", "#3498db", "#3489db"]
my_cmap = ListedColormap(color_step)
```

- 커스텀한 색상으로 강조하고 싶은 데이터를 시각화 한다
```python
def drawGraph():
    # 도화지를 펼친다
    plt.figure(figsize=(14, 10))
    
    # 그림을 그린다
    # 오차를 커스텀화한 색상으로 표현한다.
    plt.scatter(df["A"], df["B"], s=50, c=df["오차"], cmap=my_cmap)
    # 경향선을 그린다
    plt.plot(fx, f1(fx), ls="dashed", lw=3, color="g")

    # 디테일 설정
    plt.xlabel("인구수")
    plt.ylabel("CCTV")
    plt.colorbar()
    plt.grid(True)
    # 반복문을 활용하여 상위, 하위 5개를 좌표 위에 표기한다.
    for n in range(5):
        # plt.text(x좌표,y좌표,표기명)
        # 상위 5개를 좌표위에 표기해라
        # 곱하기된 숫자는 글자가 가려지지 않기 위해 조정한 값임
        plt.text(
            df_sort_f["인구수"][n] *1.02, # x 좌표
            df_sort_f["소계"][n] *0.98,  # y 좌표
            df_sort_f.index[n], # title 
            fontsize=15
        )
    
        # 하위 5개 좌표위에 표기해라
        plt.text(
            df_sort_t["인구수"][n] * 1.02, 
            df_sort_t["소계"][n] * 0.98,
            df_sort_t.index[n],
            fontsize=15
        )
        
    # 시각화를 확인한다.
    plt.show() 
drawGraph()
```

### 1.3 데이터 저장
- `df.to_csv()`
```python
# 저장
df_.to_csv("../data/ooo.csv", sep=",", encoding="utf-8")

# 확인
save = pd.read_csv("../data/ooo.csv", encoding="utf-8")
save.head()
```

---
## 1.4 기타
- `startswith()`, `endswith()`
```python
'python'.startswith('py') -> True
'python'.endswith('on') -> True
```
---

## 2. 단어 등장 빈도 시각화
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

## 3. 단어 등장 빈도 시각화 (막대그래프)

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

## 4. 워드 클라우드
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

## 5. 특정 그림 테두리 내에 워드 클라우드 그리기
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

## 6. 요약
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
