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
-
### 1.2 HTTP Response 얻기
- urlopen(URL) or request.get(URL).content

### 1.3 HTML source 얻기
- BeautifulSoup (HTTP Response, 'html.parser')

### 1.4 HTML Tag 꺼내기
- .find or find\_all ('Tag 이름', {'Attr 이름' : 'Attr 값'})

### 1.5 Tag에서 필요한 요소 꺼내기
- Tag.get_text() : 텍스트 꺼내기
- Tag.attrs : Attribute value 꺼내기



---

**웹 스크래핑**

**1\. 다음 사전**

[##_Image|kage@wYUoP/btrxB5JxAzR/Gb4ttomFNoQc2ck4ykGijK/img.png|CDM|1.3|{"originWidth":720,"originHeight":216,"style":"alignCenter"}_##]

**라이브러리 준비**

웹 스크래핑에 필요한 라이브러리를 모두 준비합니다.

```
from bs4 import BeautifulSoup 
from urllib.request import urlopen

# import requests
```

beautifulsup4 : 웹 스크래핑할 때 사용
urllib.request : URL을 가져오는데 사용
urllib.request를 사용할 때 URL에 한글이 포함되어있으면 문제가 발생할 수 있음. 이럴 때는 requests 라이브러리를 활용하여 requests.get(URL).content 사용

---

**1. URL 분석**

URL을 분석하며 패턴 존재 여부를 확인하고, query의 종류를 파악합니다.

_URL : https://alldic.daum.net/search.do?q=crawling_

  
① https://alldic.daum.net : 메인 URL  
② search.do : 함수의 역할  
③ q=crawling : 쿼리, 함수에 들어가는 파라미터 역할

---

**2\. HTTP Response, 3. **HTTP source 얻기****

```
# url 변수 생성
word = 'crawling'
url = 'https://alldic.daum.net/search.do?q=' + word

# url의 정보를 서버에서 받음
# web = requests.get(url).content
web = urlopen(url)

# 웹페이지의 HTML 구조를 파싱
web_page = BeautifulSoup(web, 'html.parser')
```

서버에서 웹페이지에 대한 정보를 얻은 후 html을 모두 가져옵니다.

---

**4. HTML Tag 꺼내기**

가져온 HTML을 태그로 접근합니다.

| Tag's name : html, head, body, h1, p, span, li, ol, ul, div   Tag's Attribute (name & value) : class, id, style, href, src |
| --- |

a = web\_page.find( 'Tag 이름' , { 'Attr 이름'  :  'Attr 값' } ) or

b = web\_page.find\_all( 'Tag 이름' , { 'Attr 이름'  :  'Attr 값' } )

find로 꺼내면 첫번째 값만 얻을 수 있습니다.

find\_all 모든 값을 불러올 수 있습니다.

이 둘의 데이터 타입은 다릅니다.

type(a) -> Tag

type(b) -> ResultSet (리스트와 유사)

---

**5\. Tag로부터 텍스트 혹은 Attribute values 꺼내기**

```
# 'crawling'
web_page.find('span', {'class' : 'txt_emph1'}).get_text(
web_page.find_all('span', {'class' : 'txt_emph1''})[0].get_text()

# {'class': ['txt_emph1']}
web_page.find('span', {'class' : 'txt_emph1''}).attrs
web_page.find_all('span', {'class' : 'txt_emph1''})[0].attrs
```

get\_text / attrs를 활용하여 태그 안의 있는 내용들을 출력한다

find\_all을 사용한 경우에는 인덱스 번호를 활용한 이후에 values를 꺼낸다.

---

**2\. 네이버 영화**

[##_Image|kage@dVEGbd/btrxr442ZO3/GfkbCkWjkeSeYNcmIFRWsK/img.jpg|CDM|1.3|{"originWidth":203,"originHeight":290,"style":"alignLeft"}_##]

위의 **1,2,3번**에 해당되는 내용들을 진행한 코드입니다.

```
from bs4 import BeautifulSoup 
from urllib.request import urlopen
# import requests

url = 'https://movie.naver.com/movie/bi/mi/basic.naver?code=92075'
web = urlopen(url)
web_page = BeautifulSoup(web, 'html.parser')

# web = requests.get(url).content
```

이제 find와 find\_all을 사용하여 필요한 내용을 추출해보도록 하겠습니다.

---

**1\. 영화 제목 스크래핑**

```
title = web_page.find('h3', {'class':'h_movie'}).find('a')

print('Movie Title:')
print(title.get_text())
```

---

**2\. 영화 줄거리 스크래핑**

```
summary = web_page.find('p', {'class': 'con_tx'})

print('Movie Summary:')
print(summary.get_text())
```

---

**3\. 감독 이름 & 출연 배우 스크래핑**

```
# 감독
director = web_page.find('div', {'class': 'dir_product'}).find('a')

print('Director:')
print(director.get_text())

# 주연 배우
actor_list = web_page.find('div', {'class': 'made_people'})
actor_names = actor_list.find_all('a', {'class':'k_name'})

for actor in actor_names:
    print(actor.get_text())
```

---

**5\. 영화 리뷰 제목 스크래핑**

```
url = 'https://movie.naver.com/movie/bi/mi/review.naver?code=208077'
web = urlopen(url)

web_page = BeautifulSoup(web, 'html.parser')

review_list = web_page.find('div', {'class':'obj_section'})
review_titles = review_list.find_all('strong')

for title in review_titles:
    print(title.get_text())
```

---

**3\. 브런치 글**

[##_Image|kage@cGfKE2/btrxIKRGpsP/UD01Gdjp2hnzZCSoTQqII0/img.png|CDM|1.3|{"originWidth":937,"originHeight":444,"style":"alignCenter"}_##]

마찬가지로 **1,2,3번**에 해당되는 내용들을 진행한 코드입니다.

```
from bs4 import BeautifulSoup 
from urllib.request import urlopen
# import requests

url = 'https://brunch.co.kr/@1015059620/14'
web = urlopen(url)
source = BeautifulSoup(web, 'html.parser')
# web = requests.get(url).content
```

---

블로그의 있는 텍스트를 txt파일에 저장하는 방법입니다.

```
with open('brunch.txt','w',encoding = 'utf-8') as f:
    
    all_text = source.find('div',{"class": "wrap_body"})
    article = all_text.find_all('p')
    
    for content in article:
        print(content.get_text())
        f.write(content.get_text() + '\n')
```

_with open("파일","모드") as sth:_

     _문장_

| r | read |
| --- | --- |
| w | write |
| a | append |

---

해당 블로거의 게시글의 10개를 불러오는 코드입니다.

```
for i in range(10):

    try: 
        url = 'https://brunch.co.kr/@1015059620/' + str(i)
        # web = requests.get(url).content
        web = urlopen(url)
        source = BeautifulSoup(web, 'html.parser')

        with open('brunch_all.txt', 'a', encoding = 'utf-8') as f:

            all_text = source.find('div',{"class": "wrap_body"})
            article = all_text.find_all('p')

            for content in article:
                print(content.get_text())
                f.write(content.get_text() + '\n')
    except:
        print('*** {}번 글 스크래핑 중 에러가 발생했습니다.'.format(i))
```

try-except 구문

---

**HTTP Request (↔ HTTP Response)**

```
import requests
requests.get(URL).content
```

\- POST 요청 : Create  
\- GET 요청 : Read  
\- PUT 요청 : Update  
\- DELETE 요청 : Delete

---

**4\. 네이버 뉴스 기사**

[##_Image|kage@biHXpx/btrxEDMTPr7/kQr3GFbMkGtm7T7TuSPDZ1/img.png|CDM|1.3|{"originWidth":882,"originHeight":591,"style":"alignCenter","width":600,"height":402}_##]

필요한 라이브러리를 준비하고 웹페이지의 html을 서버에서 받아온다.

```
import requests
from bs4 import BeautifulSoup

import pandas as pd
from datetime import datetime
import time
import re

query = '손흥민'
url = "https://search.naver.com/search.naver?where=news&query=" + query

web = requests.get(url).content
source = BeautifulSoup(web, 'html.parser')
```

**1\. 뉴스 타이틀**

```
news_titles = source.find_all('a', {'class' : 'news_tit'})

title_list = []

for title in news_titles:
    title_list.append(title.get_text())

print(title_list)
```

**2\. 뉴스 기사 링크**

```
urls_list = []

for urls in source.find_all('a', {'class' : "info"}):
    if urls.attrs["href"].startswith("https://sports.news.naver.co"):
        urls_list.append(urls.attrs["href"])
```

**3\. 단일 기사** 

urls\_list에서 링크를 추출하여 단일 기사의 html을 꺼내온다.

```
headers = {'User-Agent':'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36'}

web_news = requests.get(urls_list[0], headers=headers).content
source_news = BeautifulSoup(web_news, 'html.parser')
```

\*\* 봇이 아니라는 것을 해드태깅을 하여 알려줍니다.

[##_Image|kage@cRavoL/btrxED69441/2eLjKO40oixkf6Z59vq0h0/img.png|CDM|1.3|{"originWidth":1915,"originHeight":424,"style":"alignCenter"}_##]

(1) 기사 제목

```
title = source_news.find('h4', {'class' : 'title'}).get_text()
print(title)
```

(2) 발행 날짜

```
date = source_news.find('div', {'class' : 'info'}).find('span').get_text()

date = date.replace(" ","")

date1 = date [4:14]
date2 = date [17:]
date3 = (lambda x : 'am' if x == '오전' else 'pm')(date [15:17])
date4 = date1 + date2 + date3
```

(3) 기사 본문

```
article = source_news.find('div', {'id' : 'newsEndContents'}).get_text()

article = article.replace("\n", "")
article = article.replace("기사내용 요약", "")
article = article.replace("동영상 뉴스", "")
article = article.strip()
```

(4) 하나의 데이터프레임으로 만들기

```
# url 분석 후 bs4로 get으로 html을 받아온다.
# find, find_all로 필요한 태그들에 접근한다.
# .get_text() or .attrs로 필요한 내용을 출력한다.

# 스크래핑한 데이터를 리스트 안에 넣는다.
titles = []
dates = []
articles = []
article_urls = []
press_companies = []


# 리스트의 데이터를 이용하여 데이터 프레임을 만든다.
article_df = pd.DataFrame({'Title':titles, 
                           'Date':dates, 
                           'Article':articles, 
                           'URL':article_urls, 
                           'PressCompany':press_companies})

# 데이터를 엑셀파일로 저장한다.
article_df.to_excel('result.xlsx', index=False, encoding='utf-8')
```

\*\*strftime

```
from datetime import datetime

article_df.to_excel('result_{}.xlsx'.format(datetime.now().strftime('%y%m%d_%H%M')), index=False, encoding='utf-8')
```

%Y : 연도 4자리

%y : 연도 두자리

%m : 월

%d : 일

%h : 영문 월

%H : 시각

%M : 분

%S : 초

**4\. 여러 뉴스 데이터 모으기 (에러 회피)**

```
# 사용자에게 입력받을 값을 파라미터에 두고 함수를 생성한다.
def main_crawling(query, start_date, end_date, sort_type, max_page):
    
    if query == '':
        query = '데이터 분석'
    if len(start_date) != 10:
        start_date = '2021.01.01'
    if len(end_date) != 10:
        end_date = '2021.12.31'
    if sort_type not in ['0', '1', '2']:
        sort_type = '0'
#     if max_page == '':
#         max_page = 5


    # 쿼리에 맞는 형태로 변경해줍니다.
    start_date = start_date.replace(".", "")
    end_date = end_date.replace(".", "")

    # 각 기사들의 데이터를 담을 리스트를 생성한다.
    titles = []
    dates = []
    articles = []
    article_urls = []
    press_companies = []


	# 지정한 기간 내 원하는 페이지 수만큼의 기사를 크롤링합니다.
    current_call = 1
    last_call = (max_page - 1) * 10 + 1 # max_page이 5일 경우 41에 해당 
    

	# 함수를 반복해서 실행시킨다.
    while current_call <= last_call:

        print('\n{}번째 기사글부터 크롤링을 시작합니다.'.format(current_call))

        url = "https://search.naver.com/search.naver?where=news&query=" + query \
              + "&sort=" + sort_type \
              + "&nso=so%3Ar%2Cp%3Afrom" + start_date \
              + "to" + end_date \
              + "%2Ca%3A&start=" + str(current_call)

		# 크롤링할 url을 리스트에 담는다.
        urls_list = []
        try: # 네이버 뉴스 검색결과 페이지 자체에 접근이 불가능할 경우 에러가 발생할 수 있습니다.
            web = requests.get(url).content
            source = BeautifulSoup(web, 'html.parser')

            for urls in source.find_all('a', {'class' : "info"}):
                if urls["href"].startswith("https://news.naver.com"):
                    urls_list.append(urls["href"])
        except:
            print('해당 뉴스 검색 페이지의 네이버 뉴스 링크를 모으는 중 에러가 발생했습니다. : ', url)
        
        # urls_list : 해당 페이지에 있는 "네이버 뉴스"의 링크 모음(list)
        if urls_list != []:
            for url in urls_list:
                try: # 특정 뉴스 기사글 하나를 크롤링하는 중 에러가 발생할 수 있습니다.
                    headers = {'User-Agent':'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36'}
                    web_news = requests.get(url, headers=headers).content
                    source_news = BeautifulSoup(web_news, 'html.parser')

                    title = source_news.find('h3', {'id' : 'articleTitle'}).get_text()
                    print('Processing article : {}'.format(title))

                    date = source_news.find('span', {'class' : 't11'}).get_text()

                    article = source_news.find('div', {'id' : 'articleBodyContents'}).get_text()
                    article = article.replace("\n", "")
                    article = article.replace("// flash 오류를 우회하기 위한 함수 추가function _flash_removeCallback() {}", "")
                    article = article.replace("동영상 뉴스       ", "")
                    article = article.replace("동영상 뉴스", "")
                    article = article.strip()

                    press_company = source_news.find('address', {'class' : 'address_cp'}).find('a').get_text()

                    titles.append(title)
                    dates.append(date)
                    articles.append(article)
                    press_companies.append(press_company)
                    article_urls.append(url)
                except:
                    print('\n*** {}번부터 {}번까지의 기사글을 크롤링하는 중 문제가 발생했습니다.'.format(current_call, current_call+9))
                    print('*** 다음 링크의 뉴스를 크롤링하는 중 에러가 발생했습니다 : {}'.format(url))
        else:
            pass

        time.sleep(5)
        current_call += 10
            
            
    article_df = pd.DataFrame({'Title':titles, 
                               'Date':dates, 
                               'Article':articles, 
                               'URL':article_urls, 
                               'PressCompany':press_companies})

    article_df.to_excel('result_{}.xlsx'.format(datetime.now().strftime('%y%m%d_%H%M')), index=False, encoding='utf-8')
    
    print('\n크롤링이 성공적으로 완료되었습니다!')
    print('\n크롤링 결과를 다음 파일에 저장하였습니다 : {}'.format(datetime.now().strftime('%y%m%d_%H%M')))
    
    
    
query = input('검색어를 입력해주세요. (ex. 데이터 분석) : ')
start_date = input('검색 시작 날짜를 입력해주세요. (형식 : 2021.01.01) : ')
end_date = input('검색 종료 날짜를 입력해주세요. (형식 : 2021.12.31) : ')
sort_type = input('정렬 타입을 입력해주세요 (관련도순 = 0, 최신순 = 1, 오래된순 = 2) : ')
max_page = input('크롤링을 원하는 전체 페이지 수를 입력해주세요. (ex. 5) : ')


if start_date > end_date:
    print('\n시작 날짜는 종료 날짜보다 이후로 지정하실 수 없습니다. 다시 실행해주세요!')
elif max_page == '':
    max_page = 5
    print('\n원하시는 페이지 수가 입력되지 않았습니다. 5 페이지까지만 크롤링을 진행합니다.')
    main_crawling(query, start_date, end_date, sort_type, max_page)
else:
    max_page = int(max_page)
    main_crawling(query, start_date, end_date, sort_type, max_page)
```

---

**셀레니움**

기본 세팅

```
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

가상 브라우저 연결

```
# 자동으로 크롬드라이버(가상브라우저) 파일을 다운로드 후 세팅
service = Service(executable_path=ChromeDriverManager().install()) 

# 세팅된 크롬드라이버를 연결해 가상브라우저 실행
driver = webdriver.Chrome(service=service)

# 가상 브라우저를 최대화하고 싶을 때 활용하세요
driver.maximize_window()
```

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

\+ \[ .click() / .send\_keys('~~~') / .clear() \]

**기사 원문 전체 번역**

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
