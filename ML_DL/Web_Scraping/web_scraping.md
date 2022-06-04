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
| Tag 이름 | html, head, body, h1, p, span, li, ol, ul, div |   
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
--- 

## 4. strftime
```
from datetime import datetime
article_df.to_excel('ooo.xlsx'.format(datetime.now().strftime('%y%m%d_%H%M')), index=False, encoding='utf-8')
```

%Y : 연도 4자리   
%y : 연도 두자리   
%m : 월   
%d : 일   
%h : 영문 월   
%H : 시각   
%M : 분   
%S : 초   

---

## 4. 셀레니움
- 기본 세팅
```python
!pip install selenium==4.1.0
!pip install webdriver-manager==3.5.2

# 자동으로 크롬드라이버(가상브라우저) 파일을 다운로드해주는 라이브러리
from webdriver_manager.chrome import ChromeDriverManager

# 다운로드된 크롬드라이버 파일을 연결하기 위해 활용
from selenium.webdriver.chrome.service import Service

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

from bs4 import BeautifulSoup 
import time
import pandas as pd

import warnings
warnings.filterwarnings("ignore")
```
- 가상 브라우저 연결
```
# 자동으로 크롬드라이버(가상브라우저) 파일을 다운로드 후 세팅
service = Service(executable_path=ChromeDriverManager().install()) 

# 세팅된 크롬드라이버를 연결해 가상브라우저 실행
driver = webdriver.Chrome(service=service)

# 가상 브라우저를 최대화하고 싶을 때 활용
driver.maximize_window()
```
- 셀레니움 활용
```
# 링크이동
translate_url = 'https://translate.google.co.kr/?sl=auto&tl=en&op=translate&hl=ko' 
driver.get(translate_url)
print(driver.current_url)

# driver.current_url (HTML 받아오기)
web = BeautifulSoup(driver.page_source, 'html.parser')
web.find_all('div')[0]

origin_xpath = '/html/body/c-wiz/div/div[2]/c-wiz/div[2]/c-wiz/div[1]/div[2]/div[3]/c-wiz[1]/span/span/div/textarea'
driver.find_element_by_xpath(origin_xpath).send_keys('파이썬은 쉽습니다')

translation_xpath = '/html/body/c-wiz/div/div[2]/c-wiz/div[2]/c-wiz/div[1]/div[2]/div[3]/c-wiz[2]/div[6]/div/div[1]/span[1]/span/span'
translated_contents = driver.find_element_by_xpath(translation_xpath)
print(translated_contents.text)
```
driver.find\_element\_by\_class\_name('ooo')   
driver.find\_element\_by\_id('ooo')   
driver.find\_element\_by\_css\_selector('ooo')    
driver.find\_element\_by\_xpath('ooo')   

\+ \[.click() / .send\_keys('ㅁㅁ') / .clear()\]

- 기사 원문 전체 번역
```
eng_contents = []

service = Service(executable_path=ChromeDriverManager().install()) 
driver = webdriver.Chrome(service=service)

translate_url = 'https://translate.google.co.kr/?sl=auto&tl=en&op=translate&hl=ko' 
driver.get(translate_url) 
print(driver.current_url)
time.sleep(3)

for row_index, row in df.iterrows():
    origin_xpath = '/html/body/c-wiz/div/div[2]/c-wiz/div[2]/c-wiz/div[1]/div[2]/div[3]/c-wiz[1]/span/span/div/textarea'
    driver.find_element_by_xpath(origin_xpath).clear()
    driver.find_element_by_xpath(origin_xpath).send_keys(df['Article'][row_index])
    time.sleep(3)

    translation_xpath = '/html/body/c-wiz/div/div[2]/c-wiz/div[2]/c-wiz/div[1]/div[2]/div[3]/c-wiz[2]/div[6]/div/div[1]/span[1]/span/span'
    translated_contents = driver.find_element_by_xpath(translation_xpath).text
    eng_contents.append(translated_contents)
    print('기사글 [ {} ] 의 번역이 끝났습니다.'.format(df['Title'][row_index]))

print('전체 contents 번역이 끝났습니다!')

driver.close()
driver.quit()


df['Translated_article'] = eng_contents
df.to_excel('translation_result.xlsx', index=False, encoding='utf-8')

print('crawling_result.xlsx 파일로 전체 저장이 완료되었습니다!')
