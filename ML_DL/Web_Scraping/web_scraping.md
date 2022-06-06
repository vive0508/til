웹 스크래핑
===

### 데이터 분석를 위한 라이브러리

| **라이브러리명** | **용도** | **별칭** | **import 구문 예시** |
| --- | --- | --- | --- |
| numpy | 수치형 자료 계산 및 연산 | np | import numpy as np |
| pandas | 정형 데이터 전처리 및 분석 | pd | import pandas as pd |
| matplotlib | 데이터 차트 시각화 | plt | import matplotlib.pyplot as plt |
| seaborn | 보다 개선된 데이터 시각화 | sns | import seaborn as sns |
| \*beautifulsoup4(bs4) | 웹 데이터 추출(web scraping) |   | from bs4 import ~~ |
| nltk | 자연어 데이터 전처리 |   | import nltk |
| scikit-learn | 전통적인 머신러닝 알고리즘 |   | from sklearn import ~~ |

---

## 1. 웹 스크래핑 진행단계

1. URL 분석
2. HTTP Response 얻기 : urlopen(URL) or request.get(URL).content
3. HTML source 얻기 : BeautifulSoup (HTTP Response, 'html.parser')
4. HTML Tag 꺼내기 : .find or find\_all ('Tag 이름', {'Attr 이름' : 'Attr 값'})
5. Tag로부터 텍스트 혹은 Attribute values 꺼내기 : Tag.get_text() or Tag.attrs

```python
import re  
import pandas as pd 
import numpy as np
import googlemaps
import folium

from bs4 import BeautifulSoup
from urllib.request import Request, urlopen 
from fake_useragent import UserAgent
from urllib.parse import urljoin 

from tqdm import tqdm 
```

### 1.1 URL 분석
- URL을 분석하며 패턴 존재 여부를 확인하고, query의 종류를 파악한다.   
- 함수의 역할을 하는 것이 무엇인지, 파라미터 역할을 하는 query가 어떤 것이 있는지 무엇인지 확인한다.   
- 주소에 한글이 포함된 경우에 하기 코드를 사용한다.
```
# url 디코드를 검색하여 이용하거나,
# format 함수를 사용하여 원하는 검색어로 검색한다.
import urllib
form urllib.request import urlopen, Request

url = 'http://www.ooo.com/search/{search_keyword}'
req = Request(url.format(search_keyword=urllib.parse.quote('검색어')))

response = urlopen(req)

soup = BeautifulSoup(response, 'html.parser')
```
- url을 합쳐야 할 경우 하기 코드를 사용한다
```
# 모듈을 임포트한다
from urllib.parse import urljoin

# 상대주소와 절대주소에 대해 잘 대응해준다
# 상대 주소를 절대주소로 변환해준다
# 절대주소를 지정해주어야 한다
urljoin(url_base, url_sub)
```

### 1.2 HTTP Response 얻기
- 서버에서 웹페이지에 대한 정보를 얻은 후 html을 모두 가져온다.
```python
# url 변수 생성 (url 분석에서 파악한 패턴을 적용해볼 수 있음)
url = '사이트 주소' + query

# url의 정보를 서버에서 받음 (from urllib.request import urlopen 사용시)
# 변수명을 response, res, page와 같은 변수명으로 많이 사용
res = urlopen(url)

# url의 정보를 서버에서 받음 (urllib.request 사용시)
res = requests.get(url).content
```

- 정상적으로 가져왔는지 확인
```python
res.status
```

### 1.3 HTML source 얻기
```
# 웹페이지의 HTML 구조를 파싱
html = BeautifulSoup(res, 'html.parser')

# 좀 더 깔끔한 형태로 볼 수 있는 방법
print(html.prettify())
```

### 1.4 HTML Tag 꺼내기
- head, body 접근(참고)
```
html.head
html.body
```

- HTML 태그에 접근한다.   

| 구분 | 내용 |   
| :--: | :-- |   
| Tag 이름 | html, head, body, h1, p, span, li, ol, ul, div, a |   
| Tag Attribute | class, id, style, href, src |   

- .find or find_all ('Tag 이름', {'Attr 이름':'Attr 값'})   
- .find or find_all ('Tag 이름', {'Attr 이름':'Attr 값','Attr 이름':'Attr 값'}) (다중조건)   
```python
# 1 : html.find.Tag이름
# 2 : html.find('Tag이름')
# 3 : html.find('Tag이름',{'Attr이름':'Attr 값'})
# 4 : html.find('Tag이름', Attr이름_='Attr값')
# 5 : html.find('Tag이름','Attr값')
# 6 : html.find(Attr이름_='Attr값')
# 7 : html.select_one(".클래스이름")
# 8 : html.select_one("#Id이름")

# find로 꺼내면 첫번째 값만 얻을 수 있다.
a = response.find('Tag이름', {'Attr 이름':'Attr 값'})
type(a) -> Tag

# find_all 모든 값을 불러올 수 있다
# iterable하기 때문에 반복문과 같이 사용된다
b = html.find_all('Tag이름',{'Attr이름':'Attr 값'})
type(b) -> ResultSet (리스트와 유사)
```
- select_one, select
```python
# find, select_one : 단일 선택
# find_all, select : 다중 선택 

res = requests.get(url)
html = BeautifulSoup(response, "html.parser") 

html.select("#id이름")
html.select("#id이름 > 하위 태그이름")
html.select(".class이름")
html.select(".class이름.class이름")
```

### 1.5 Tag로부터 텍스트 혹은 Attribute values 꺼내기
- Tag.get_text(), Tag.attrs
```
# Tag.get_text() : 텍스트 꺼내기
# 1.Tag.text
# 2.Tag.string
# 3.Tag.get_text() 
html.find('Tag 이름',{'Attr 이름':'Attr 값'}).get_text()
html.find_all('Tag 이름',{'Attr 이름':'Attr 값'})[0].get_text()

# Tag.attrs : Attribute value 꺼내기
html.find('span', {'class' : 'txt_emph1''}).attrs
html.find_all('span', {'class' : 'txt_emph1''})[0].attrs

# 링크를 꺼내는 방법
1. Tag.find("a").attrs["href"]
2. Tag.find("a")["href"]
3. Tag.select_one("a").get("href")
```
find_all을 사용한 경우에는 인덱스 번호를 활용한 이후에 values를 꺼낸다.   
 
- 문자 추출 후 정리
```
str.strip() : 공백 제거
str.replace('A','a') : 변경
```
- re 모듈
```
import re 

# text를 \n 또는 \r\n 기준으로 나누어서 리스트로 만들어라
text = Tag.get_text()
re.split(("\n|\r\n"), text))

# 정규표현식
re.search("정규표현식", str).group()
```
- urljoin 모듈
```python
from urllib.parse import urljoin  
urljoin(url_base, Tag.find("a")["href"])
```

---

## 2. HTTP 상태

- http 상태 코드 : 요청과 응답이 잘 이루어졌는지 확인
```
# 정상일 경우 200
import requests
response = requests.get(URL).content
response.status
```
200

- 403 코드 에러
```python
# 봇이 아니라는 것을 해드태깅을 하여 알려주어야 한다.
!pip install fake-useragent

from urllib.request import Request, urlopen 
from fake_useragent import UserAgent
from bs4 import BeautifulSoup

# 1. req = Request(url, headers={"user-agent": "Chrome"})
# 2. req = Request(url, headers={"user-agent": 'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36'}
# 3.

# fake-useragent
ua = UserAgent
req = Request(url, headers={"user-agent": ua.ie})

res = urlopen(req)
html = BeautifulSoup(web_news, 'html.parser')
```

---

## 3. 저장
### 3.1 엑셀 저장
- df = pd.DataFrame(data) : 데이터프레임으로 변환
- df.to_excel('ooo.xlsx', encoding='utf-8')

### 3.2 텍스트를 txt 파일에 저장하는 방법
- with 구문 활용
- with open("파일","모드") as sth:
| 모드 | 기능 |
| :--: | :--: |
| r | read |
| w | write |
| a | append |

```python
from bs4 import BeautifulSoup 
from urllib.request import urlopen

res = urlopen(url)
response = BeautifulSoup(res, 'html.parser')

with open('test.txt','w',encoding = 'utf-8') as f:
    all_text = response.find('Tag 이름', {'Attr 이름':'Attr 값'})
    article = all_text.find_all('Tag 이름')
    
    for content in article:
        print(content.get_text())
        f.write(content.get_text() + '\n')
```
- 여러 게시글의 텍스트를 가져와서 저장하는 방법
```
for i in range(10):
    try: 
        # 반복문으로 페이지를 넘긴다
        url = 'url 주소' + str(i)
        # res = requests.get(url).content
        res = urlopen(url)
        response = BeautifulSoup(res, 'html.parser')

	# 텍스트를 저장한다
        with open('test.txt', 'a', encoding = 'utf-8') as f:
	    all_text = response.find('Tag 이름', {'Attr 이름':'Attr 값'})
	    article = all_text.find_all('Tag 이름')

	    for content in article:
		print(content.get_text())
		f.write(content.get_text() + '\n')

    # try-except 구문으로 예외 발생 확인
    except:
        print('*** {}번 글 스크래핑 중 에러가 발생했습니다.'.format(i))
```


