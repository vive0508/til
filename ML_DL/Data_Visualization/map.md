지도 시각화
===

## 1. Google Maps
- 터미널에서 콘다 명령어로 googlemaps library 설치([링크](https://anaconda.org/conda-forge/googlemaps))
- conda install -c conda-forge googlemaps
- !pip install googlemaps==4.6.0
- 구글 클라우드 플랫폼에서 API 연결
```
import googlemaps  
gmaps = googlemaps.Client(key="personal\_key")

tmpMap = gmaps.geocode('보라매공원', language="ko")  
tmpMap
```

___

## 2. folium 라이브러리
### 2.1 라이브러리 설치 및 불러오기
```python
# 설치
!pip install folium==0.5.0

# 안되면 아래의 라이브러리도 설치
!pip install charset 
!pip install charset-normalizer

# 불러오기
import folium
import pandas as pd 
import json 
```

### 2.2 folium 기본 형태
```python
# folium에서 Map이라는 클래스를 사용   
# location : 초기 지도 center 위치 (위도, 경도)    
# zoom start : 줌 크기   

m = folium.Map(location=[위도, 경도], zoom_start=14)
```

### 2.3 tiles 옵션
- OpenStreetMap   
- Mapbox Bright   
- Mapbox Control Room   
- Stamen(Terrain, Toner, and Watercolor)    
- Cloudmade    
- Mapbox    
- CartoDB      
```python
# tiles : 지도 타입

m = folium.Map(
    location=[위도, 경도], 
    zoom_start=14,
    tiles="OpenStreetMap"
)
```
___

### 2.4 마커 생성
#### 2.4.1 `folium.Marker()` 기본 형태
```python
m = folium.Map(
    location=[위도, 경도], 
    zoom_start=14,
    tiles="OpenStreetMap"
)

folium.Marker((위도, 경도)).add_to(m)
```
#### 2.4.2 `folium.Marker()` 옵션
- [https://fontawesome.com/v5.15/icons?d=gallery&p=2&m=free](https://fontawesome.com/v5.15/icons?d=gallery&p=2&m=free) 
- [https://getbootstrap.com/docs/3.3/components/](https://getbootstrap.com/docs/3.3/components/)
```python
# popup : 클릭하면 나오는 것
# tooltip : 마우스 커서가 닿으면 나오는 것
# prefix : fa 혹은 glyphicon를 입력해야 사용할 수 있는 아이콘이 있다

folium.Marker(
    location=[위도, 경도],
    popup="클릭하면 나옵니다",
    tooltip="마우스가 닿으면 나옵니다",
    icon=folium.Icon(
        color="blue",
        icon_color="white",
        icon="glyphicon glyphicon-cloud",
        angle=50, 
        prefix="glyphicon") # prefix : fa or glyphicon
).add_to(m)
```

___

### 2.5 `folium.ClickForMarker()
- 마우스 클릭시 마커 생성
```python
m = folium.Map(
    location=[위도, 경도], 
    zoom_start=14,
    tiles="OpenStreetMap"
)

m.add_child(folium.ClickForMarker(popup="ClickForMarker"))
```

### 2.6 `folium.LatLngPopup()`
- 마우스 클릭시 위도, 경도 값 반환
```python
m = folium.Map(
    location=[위도, 경도], 
    zoom_start=14,
    tiles="OpenStreetMap"
)

m.add_child(folium.LatLngPopup())
```


### 2.7 `folium.Circle()`, `folium.CircleMarker()`
- 원형 
```python
m = folium.Map(
    location=[위도, 경도], 
    zoom_start=14,
    tiles="OpenStreetMap"
)

# Circle 
folium.Circle(
    location=[위도, 경도],
    radius=100, # 반지름
    fill=True, # 원 색칠
    color="#eb9e34", # 선의 색상
    fill_color="red", # 원의 색상
    popup="Circle Popup",
    tooltip="Circle Tooltip"
).add_to(m)

# CircleMarker
folium.CircleMarker(
    location=[위도, 경도],
    radius=100, # 반지름
    fill=True, # 원 색칠
    color="#34ebc6", # 선의 색상
    fill_color="#c634eb", # 원의 색상
    popup="CircleMarker Popup",
    tooltip="CircleMarker Tooltip"
).add_to(m)
```
___

### 2.8 html로 저장
```python
m.save("./folium.html")
```
___

## 3. Choropleth map : 행정구역별로 색칠해놓은 지도
- 지도 시각화 : Folium library 활용   
- 지도 데이터 : GeoJSON 활용   

### 3.1 json 파일
#### 3.1.1 json
- Javascript Object Notation   
- 데이터 교환을 위한 표준 포맷   
- XML, YAML는 json 이전의 표준 포맷   
```python
# 불러오는 것은 load, 저장하는 것은 dump
import json

geo_path = '파일명.json'
geo_str = json.load(open(geo_path, 'r' , encoding='utf-8'))
```

#### 3.1.2 pyptny
- JSON 구조를 쉽게 파악할수 있게 해주는 도구   
```python
# pyptny 설치
!pip install pyprnt==2.3.3

# pyptny 임포트
from pyprnt import prnt

# ptptny 활용법
# truncate : 안에 있는 내용이 너무 길면 잘라줌
# width : 내용이 찌그러질 때 조절

print(json 자료, truncate=True, width=80)
```

## 3.2 Choropleth map
```python
import json

geo_path = '파일명.json'
geo_str = json.load(open(geo_path, 'r' , encoding='utf-8'))

map.choropleth(geo_data = geo_str, # 가져온 JSON 파일(지도 좌표)
                     data = df, # 시각화의 대상이 될 Series or DataFrame
                     # columns = ['열이름1', '열이름2']
                     columns = [df['열이름1'], df['열이름2']] # DataFrame columns (가져올 열이 인덱스 열일 때는 df.index)
                     key_on = 'feature.id'  # GeoJSON 규약을 따름
                     fill_color = 'PuRd' 
                     fill_opacity=0.5, # 0~1 
                     line_opacity=0.2, # 0~1 
                     legend_name="범례명"    
).add_to(m)
```

