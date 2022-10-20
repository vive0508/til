셀레니움(Selenium)
===

## 1. 셀레니움

### 1.1 셀레니움을 사용할 경우
- 웹 브라우저의 주소를 정확히 모를 때 (bs에서는 정확히 알고 있어야 가능)
- 동적 페이지(자바스크립트를 사용하는)에 접근해서 정보를 가져올 경우 사용한다.
- 스크롤, 글자입력, 클릭, 캡처 등 웹 브라우저를 제어할 수 있다. 

---

## 2. 셀레니움 활용
- 셀레니움 설치
```python
# 셀레니움 설치
conda install selenium

# 모듈 임포트
from selenium import webdriver
```
- 세팅된 크롬드라이버를 연결해 가상브라우저 실행
```python
driver = webdriver.Chrome("../driver/chromedriver.exe")
```
- 원하는 주소로 이동
```python
url = 'https://ooo.com/' 
driver.get(url)
print(url)
```
- 팝업창 때문에 해당 URL로 접근이 안될때
```python
# 팝업창 화면 전환 후 닫아주기 
driver.switch_to_window(driver.window_handles[-1])
driver.close()

# 다시 메인창으로 전환
driver.switch_to_window(driver.window_handles[-1])

# 해당 url로 접근
driver.get(url)
```
- 새로고침
```python
driver.refresh()
```

- 현재 브라우저 창 크기, 위치
```python
# 현재 브라우저 창 크기 
driver.get_window_size()

# 현재 브라우저 위치
driver.get_window_position()

# 현재 브라우저 창크기, 위치
driver.get_window_rect()
```
- 브라우저 크기 조절
```python
# 브라우저 창 크기 조절 
driver.set_window_size(1920, 1080)

# 화면 최대화 
driver.maximize_window() 

# 화면 최소화 
driver.minimize_window()
```
- 스크롤
```python
# 스크롤 가능한 높이
# 자바스크립트 코드 실행 : driver.execute_script()
driver.execute_script("return document.body.scrollHeight")

# 화면 스크롤 (하단 이동)
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")

# 화면 스크롤 (상단 이동) 
driver.execute_script("window.scrollTo(0, 0);")
```
- 스크린샷
```python
driver.save_screenshot("./저장경로.png")
```
- 특정 태그 지점까지 스크롤 하는 코드
```
from selenium.webdriver import ActionChains

# 특정 위치를 잡아주고
# driver.find_element_by_css_selector('css_selector')
# driver.find_element_by_id('id')
some_tag = driver.find_element_by_xpath('xpath')

# 이동시키는 방법
action = ActionChains(driver)
action.move_to_element(some_tag).perform()
```
- 특정 위치 텍스트 확인
```python
# 특정 위치를 잡아주고
# raw_data = driver.find_element_by_css_selector('css_selector')
# raw_data = driver.find_element_by_id('id')
raw_data =  driver.find_element_by_xpath('xpath')

raw_data.text
```
- 특정위치 attr 확인
```python
Tag = find_elements_by_tag_name("ooo")
Tag.get_attribute("xxx")
```

- 특정 위치 텍스트 확인
```python
# 특정 위치를 잡아주고
# raw_data = driver.find_element_by_css_selector('css_selector')
# raw_data = driver.find_element_by_id('id')
raw_data =  driver.find_element_by_xpath('xpath')

raw_data.text
```
- 입력창에 글자 넣기
```python
# 원하는 지점의 태그가 화면에 보여야 가능하다
# 새로 입력하면 뒤에 추가로 붙음 
some_tag = driver.find_element_by_xpath('xpath')
some_tag.send_keys("검색어")

# 초기화 
some_tag.clear()
```
- 클릭하기
```python
# driver.find_element_by_css_selector('css_selector').click()
# driver.find_element_by_id('id').click()

driver.find_element_by_xpath(xpath).click()
```
- 현재 화면의 html 코드 가져오기
```python
# BeautifulSoup와 함께 사용할 수 있음
from bs4 import BeautifulSoup

req = driver.page_source
soup = BeautifulSoup(req, "html.parser")
```
- 뒤로가기, 앞으로 가기
```python
driver.back()
driver.forward()
```
- 종료하기
```python
driver.close()
driver.quit()
```

### 2.1 셀레니움 vs BeautifulSoup
- find.element_by_css_selector == find, select_one
- find.elements_by_css_selector == find_all, select


