---
layout: single
title: "파이썬 웹 스크래핑"
date: 2025-01-30
last_modified_at: 2025-01-30
categories:
  - python web scraping
tags:
  - python
author: hyuna
sidebar:
  nav: "categories"
---

# 파이썬 웹 스크래핑 정리

## **1. 웹 스크래핑 vs 웹 크롤링**

| **구분**      | **웹 스크래핑**                                                | **웹 크롤링**                                              |
|---------------|---------------------------------------------------------------|-----------------------------------------------------------|
| **목적**      | 특정 웹페이지에서 필요한 데이터 추출                         | 웹 페이지 링크를 따라가며 정보 수집, 검색엔진 활용         |
| **도구**      | Beautiful Soup, Scrapy, Selenium 등 파이썬 라이브러리         | Googlebot 같은 검색엔진 크롤러, 사용자 지정 크롤러        |
| **특징**      | 주로 구조화된 데이터 수집에 사용                              | 스크래핑보다 광범위한 데이터 수집                          |
| **방식**      | HTML 특정 요소를 선택하여 그 안의 데이터만 추출              | 웹의 링크 구조를 따라 웹 페이지 방문하여 정보 수집         |



## **2. 파서 종류** 
- **html.parser** : 간단하고 쉬우나 느릴 수 있음.
- **lxml** : 빠름. 별도 설치 필요
- **html5lib** : 웹 브라우저가 HTML5를 처리하는 방식을 모방. 별도 설치 필



## **3. Beautiful Soup**
- HTML과 XML 파일에서 데이터 추출을 위한 파이썬 라이브러리
- **pip install beautifulsoup4** 로 별도 설치 필요
- **웹 스크래핑 프로세스** 
    1) HTML 가져오기
    2) Beautiful Soup 객체 생성
    3) 데이터 추출



## **4. Beautiful Soup로 HTML 문서 파싱**
1) HTML 문서 
```python
from bs4 import BeautifulSoup

# 간단한 HTML 문서
html_doc = """
<html>
<head>
    <title>The Dormouse's story</title>
</head>
<body>
    <div data-role="page" data-last-modified="2022-01-01" data-foo="value">This is a div with data attributes.</div>
    <p class="title"><b>The Dormouse's story</b></p>
    <p class="story">Once upon a time there were three little sisters; and their names were
    <a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
    <a href="http://example.com/lacie" class="sister" id="link2" data-info="more info">Lacie</a> and
    <a href="http://example.com/tillie" class="sister" id="link3" data-info="even more info">Tillie abcd</a>
    ; and they lived at the bottom of a well.</p>
    <p class="story">...</p>
</body>
</html>
"""

# HTML 문서를 Beautiful Soup 객체로 변환
# html.parser 파서 사용
soup = BeautifulSoup(html_doc, 'html.parser')

# 문서를 예쁘게 출력
print(soup.prettify())
```

2) **해당 html 문서 데이터 구조 탐색**
    (1) **print(soup.title)** : <title> 태그 찾기
    (2) **print(soup.title.name)** : <title> 태그 이름
    (3) **print(soup.title.string)** : <title> 태그의 텍스트 내용
    (4) **print(soup.title.parent.name)** : 태그의 부모 태그인 <head> 가리키고, name 은 태그의 이름 반환 = head
    (5)**print(soup.p)**: 첫번째 <p> 태그
    (6) **print(soup.p['class'])** : 첫 번째 p태그 찾고 class 속성값 가져온 후 리스트 형태로 반환 (여러 개의 클래스값을 가질 수 있으므로) = ['title']
    (7)**print(soup.find_all('a'))**: 모든 <a>태그 찾아 리스트로 반환



## **5. Beautiful Soup 메서드**
- **find_all()**: 지정된 태그의 모든 자손 검색 및 설정된 필터에 맞는 모든 결과 검색하여 리스트로 반환
- **find()**
    - 하나의 결과만 찾고 싶을 때 사용. 
    - 찾지 못했을 때 None 반환.
- **get_text()**
    - 문서나 태그 안에 인간이 읽을 수 있는 텍스트만 원할 경우 사용
    - 기본적으로 페이지 모든 텍스트 출력



## **6. CSS selectors**
1) **select()** =find_all()
    : 일치하는 모든 요소의 ResultSet 객체. 없다면 빈 ResultSet 반환
2) **select_one()**: 일치하는 요소 중 첫 번째 요소. 없다면 None 반환
