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

## 1. 웹 스크래핑 진행단계**

1. URL 분석
2. HTTP Response 얻기 : urlopen(URL) or request.get(URL).content
3. HTML source 얻기 : BeautifulSoup (HTTP Response, 'html.parser')
4. HTML Tag 꺼내기 : .find or find\_all ('Tag 이름', {'Attr 이름' : 'Attr 값'})
5. Tag로부터 텍스트 혹은 Attribute values 꺼내기 : Tag.get_text() or Tag.attrs

```python
# beautifulsup4 : 웹 스크래핑할 때 사용
from bs4 import BeautifulSoup 

# urllib.request : URL을 가져오는데 사용
from urllib.request import urlopen

# urllib.request를 사용할 때 URL에 한글이 포함되어있으면 문제가 발생할 수 있음.
# 이럴 때는 requests 라이브러리를 활용하여 requests.get(URL).content 사용
import requests
```

### 1.1 URL 분석
- URL을 분석하며 패턴 존재 여부를 확인하고, query의 종류를 파악한다.   
- 함수의 역할을 하는 것이 무엇인지, 파라미터 역할을 하는 query가 어떤 것이 있는지 무엇인지 확인한다.

### 1.2 HTTP Response 얻기
- 서버에서 웹페이지에 대한 정보를 얻은 후 html을 모두 가져온다.
```python
# url 변수 생성 (url 분석에서 파악한 패턴을 적용해볼 수 있음)
url = '사이트 주소' + query

# url의 정보를 서버에서 받음 (from urllib.request import urlopen 사용시)
web = urlopen(url)

# url의 정보를 서버에서 받음 (urllib.request 사용시)
web = requests.get(url).content
```
### 1.3 HTML source 얻기
```
# 웹페이지의 HTML 구조를 파싱
web_page = BeautifulSoup(web, 'html.parser')
```

### 1.4 HTML Tag 꺼내기
- HTML 태그에 접근한다.

| 구분 | 내용 |   
| :--: | :-- |   
| Tag 이름 | html, head, body, h1, p, span, li, ol, ul, div |   
| Tag Attribute | class, id, style, href, src |   

- .find or find_all ('Tag 이름', {'Attr 이름':'Attr 값'})
```python
# find로 꺼내면 첫번째 값만 얻을 수 있다.
a = web_page.find('Tag 이름', {'Attr 이름':'Attr 값'})
type(a) -> Tag

# find_all 모든 값을 불러올 수 있다.
b = web_page.find_all('Tag 이름',{'Attr 이름':'Attr 값'})
type(b) -> ResultSet (리스트와 유사)
```

### 1.5 Tag로부터 텍스트 혹은 Attribute values 꺼내기
- Tag.get_text(), Tag.attrs
```
# Tag.get_text() : 텍스트 꺼내기   
web_page.find('Tag 이름',{'Attr 이름':'Attr 값'}).get_text()
web_page.find_all('Tag 이름',{'Attr 이름':'Attr 값'})[0].get_text()

# Tag.attrs : Attribute value 꺼내기
web_page.find('span', {'class' : 'txt_emph1''}).attrs
web_page.find_all('span', {'class' : 'txt_emph1''})[0].attrs
```
find_all을 사용한 경우에는 인덱스 번호를 활용한 이후에 values를 꺼낸다.   

---

## 2. txt 저장

### 2.1 텍스트를 txt 파일에 저장하는 방법
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

web = urlopen(url)
source = BeautifulSoup(web, 'html.parser')

with open('test.txt','w',encoding = 'utf-8') as f:
    all_text = source.find('Tag 이름', {'Attr 이름':'Attr 값'})
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
        # web = requests.get(url).content
        web = urlopen(url)
        source = BeautifulSoup(web, 'html.parser')

	# 텍스트를 저장한다
        with open('test.txt', 'a', encoding = 'utf-8') as f:
	    all_text = source.find('Tag 이름', {'Attr 이름':'Attr 값'})
	    article = all_text.find_all('Tag 이름')

	    for content in article:
		print(content.get_text())
		f.write(content.get_text() + '\n')

    # try-except 구문으로 예외 발생 확인
    except:
        print('*** {}번 글 스크래핑 중 에러가 발생했습니다.'.format(i))
```
---
## 3. 기타
### 3.1 네이버 기사
- 봇이 아니라는 것을 해드태깅을 하여 알려주어야 한다.
```python
headers = {'User-Agent':'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36'}

web_news = requests.get(url, headers=headers).content
source_news = BeautifulSoup(web_news, 'html.parser')
```

### 3.2 HTTP Request (↔ HTTP Response)
```
import requests
requests.get(URL).content
```

- POST 요청 : Create  
- GET 요청 : Read  
- PUT 요청 : Update  
- DELETE 요청 : Delete

### 3.3 strftime
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
