---
layout: single
title:  "[멋사] Python 미니 프로젝트"
---

[멋쟁이사자처럼 8기 python 교육] Web Crawling, API, 번역, 메일 보내기

오늘은 python 모듈을 통해 활용할 수 있는 다양한 기능들을 미니프로젝트 형식으로 진행했다. 



### Web Crawling
    크롤러를 사용해 웹 페이지의 데이터를 추출해내는 행위
    
    모듈: 함수, 클래스, 변수 등이 모여있는 키트
    
    모듈 사용법: 
        1. request 모듈에서
        2. get 함수를 불러와서
        3. 요청을 보내줘. 
    


```python
import requests # 모듈 불러오기 
print(requests)

import requests

url = "https://www.notion.so/likelion-aischool/AI-SCHOOL-8-b93bee5a6c4d49ab83a024d1ad5222d4"
response = requests.get(url) 

print(response.text)
```

    <module 'requests' from 'C:\\Users\\mnch\\miniconda3\\lib\\site-packages\\requests\\__init__.py'>
    

### beautifulsoup


```python
import requests
from bs4 import BeautifulSoup

url = "http://www.daum.net/"
response = requests.get(url)

# 두 코드는 같은 내용을 출력하는 것같지만 다르다. 
# print(response.text)
# print(BeautifulSoup(response.text, 'html.parser'))
```


```python
# 확인해보자.
print(type(response.text))
print(type(BeautifulSoup(response.text, 'html.parser')))

# 결과: beautifulsoup을 사용하면 문자열을 모두 분석하기 좋게 정리 해놓는 것.
# reponse는 통 문자열임. 
```

    <class 'str'>
    <class 'bs4.BeautifulSoup'>
    

#### beautifulsoup의 사용용도 

    BeautifulSoup(데이터, 파싱방법)  # 실제 코드 예시 BeautifulSoup(response.text, 'html.parser')
        데이터: html, xml (request를 통해 받아옴.) 
        파싱방법: parsing(뭉쳐져있는 데이터를 의미있는 데이터로 변경) ex) html.parser 
        


```python
url = "http://www.naver.com/"
response = requests.get(url)


soup = BeautifulSoup(response.text, 'html.parser') 

soup.title                    # soup에서 title 태그를 출력하라. 
soup.title.string             # soup에서 title 태그의 데이터값만 출력하라. 
# print(soup.findAll('span'))   # 모든 span 태그를 출력하라.
print(soup.span)
```

    <span>뉴스스탠드 바로가기</span>
    


```python
# html문서에서 모든 a태그를 가져오는 코드 
from bs4 import BeautifulSoup
import requests

url = "http://www.naver.com/"
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')

# file = open("daum.html","w")
# file.write(response.text)
# file.close()

# print(soup.title)
# print(soup.title.string)
# print(soup.span)
# print(soup.findAll('span'))

# html 문서에서 모든 a태그를 가져오는 코드
print(soup.findAll("a"))
```

    [<a href="#newsstand"><span>뉴스스탠드 바로가기</span></a>, <a href="#themecast"><span>주제별캐스트 바로가기</span></a>, <a href="#timesquare"><span>타임스퀘어 바로가기</span></a>, <a href="#shopcast"><span>쇼핑캐스트 바로가기</span></a>, <a href="#account"><span>로그인 바로가기</span></a>, <a class="_3h-N8T9V" data-clk="dropbanner1b" href="https://whale.naver.com/banner/details/darkmode?=main&amp;wpid=RydDy7"></a>, <a class="_2aeXMlrb BMgpjddw" data-clk="dropdownload1b" href="https://installer-whale.pstatic.net/downloads/banner/RydDy7/WhaleSetup.exe" id="NM_whale_download_btn"><span style="background-color: #03bc93">다운로드</span></a>, <a class="special_logo_link" data-clk="top.spe" href="https://search.naver.com/search.naver?where=nexearch&amp;sm=top_brd&amp;fbm=0&amp;ie=utf8&amp;query=%EB%8F%99%EC%A7%80" title="동지">
    <img alt="동지" class="special_img_fold" height="60" src="https://s.pstatic.net/static/www/mobile/edit/20221222/mobile_103146290202.png" width="58"/>

#### 예쁘게 출력하기 


```python
from datetime import datetime
headers = {'User-Agent':'Mozilla/5.5 (Windows NT 6.3; Win64; x64) AppleWebkit/537.36(KHTML, like Gecko) Chrom/63.0.3239.132 Safari/537.36'}

url = "https://news.naver.com/main/main.naver?mode=LSD&mid=shm&sid1=105"
response = requests.get(url,headers=headers)

soup = BeautifulSoup(response.text,'html.parser')

results = soup.findAll('span','cluster_head_sub_topic')

for result in results:
    print(result.get_text(), "\n")

```

    알뜰폰 도매대가 낮출까  
    
    만족도 1위 KB리브엠  
    
    대전-전남-경남 우주산업 클러스터 지정  
    
    우주산업클러스터 3각체제 확정  
    
    네이버 D2SF  
    
    100번째 스타트업 투자처  
    
    과기정통부 이음5G 주파수 공급  
    
    대학·방산 분야로 확대 적용  
    
    첫 민간 우주발사체 한빛-TLV  
    
    시스템 오류로 불발  
    
    고리 3호기 원자로 자동정지  
    
    원안위 조사 착수  
    
    서비스 클라우드 전환 업무협약  
    
    상상인저축은행 - NHN클라우드  
    
    KT "AI 반도체 드림팀" 결성  
    
    내년 글로벌 시장 진출  
    
    


```python
from bs4 import BeautifulSoup
import requests
from datetime import datetime

headers = {'User-Agent':'Mozilla/5.5 (Windows NT 6.3; Win64; x64) AppleWebkit/537.36(KHTML, like Gecko) Chrom/63.0.3239.132 Safari/537.36'}
url = "https://news.naver.com/main/main.naver?mode=LSD&mid=shm&sid1=105"
response = requests.get(url,headers=headers)
soup = BeautifulSoup(response.text,'html.parser')

rank = 1

results = soup.findAll('span','cluster_head_sub_topic')

print(datetime.today().strftime("%y년 %m월 %d일의 네이버 IT 뉴스 헤드토픽\n"))
for result in results:
    print(rank,":",result.get_text())
    rank += 1
```

    22년 12월 22일의 네이버 IT 뉴스 헤드토픽
    
    1 : 토종 OTT 웨이브 
    2 : 미주 플랫폼 코코와 인수 
    3 : 대전-전남-경남 우주산업 클러스터 지정 
    4 : 우주산업클러스터 3각체제 확정 
    5 : 서비스 클라우드 전환 업무협약 
    6 : 상상인저축은행 - NHN클라우드 
    7 : 첫 민간 우주발사체 한빛-TLV 
    8 : 시스템 오류로 불발 
    9 : 카카오엔터 북미법인 래디쉬 웹소설 
    10 : 낮엔 회사원 밤엔 작가 
    11 : 네이버 D2SF 
    12 : 100번째 스타트업 투자처 
    13 : 연구소 블라인드 채용 폐지 
    14 : 1월부터 새 기준 적용 
    15 : 과기정통부 이음5G 주파수 공급 
    16 : 대학·방산 분야로 확대 적용 
    

###  (API 사용해 날씨 정보를 출력해보자. )
    api: 60c7ab245b89899ec83dd8acbdf5b8f2
    
    - API란? 
        API를 만든다 = 사용자가 필요한 기능을 만들고, 서버에 올려 특정한 규율에 따라 사용할 수 있도록 하는 것. 
        API는 기존 프로그램과 사용자가 만드는 프로그램을 연결해주는 다리와 같은 역할을 한다. 
        우리는 API를 만들지 않고, 누군가 만들어놓은 openAPI를 사용해 날씨 정보를 가져올 것이다. 
    
    - API key
        만들어진 API를 사용하는 사용자가 누구인지 알려주는 키
     

   
- API 링크 만들기  
    f-string: 문자열 안에 원하는 변수를 할당시킬 수 있다. 
    url에서 ?을 기준으로 파라미터 추가 가능, 이들은 &을 통해 연결.



```python
# API 불러오고, key, 파라미터 입력하기 
import requests
import json 
city = "Seoul"
apikey = '60c7ab245b89899ec83dd8acbdf5b8f2'
api = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={apikey}" # 중가로 사용 유의 / ? 기준으로 url 파라미터 
```


```python
# 불러온 값 확인하기 
result = requests.get(api)
print(result.text)
print(type(result.text))
```

    {"coord":{"lon":126.9778,"lat":37.5683},"weather":[{"id":803,"main":"Clouds","description":"broken clouds","icon":"04d"}],"base":"stations","main":{"temp":266.81,"feels_like":259.81,"temp_min":265.84,"temp_max":266.81,"pressure":1010,"humidity":75,"sea_level":1010,"grnd_level":1003},"visibility":10000,"wind":{"speed":6.32,"deg":311,"gust":14.13},"clouds":{"all":69},"dt":1671696518,"sys":{"type":1,"id":5509,"country":"KR","sunrise":1671662609,"sunset":1671697037},"timezone":32400,"id":1835848,"name":"Seoul","cod":200}
    <class 'str'>
    

    json 포맷을 통해 보기 쉽게 만들고,
    json을 활용해 필요한 데이터만 뽑기    


```python
import json
data = json.loads(result.text)
type(data)
```




    dict




```python
print(data["name"],"의 날씨입니다.")
print("날씨는 ",data["weather"][0]["main"],"입니다.")
print('현재온도는', data['main']['temp'],'입니다.' )
print('하지만 체감온도는', data['main']['feels_like'], '입니다.')
```

    Seoul 의 날씨입니다.
    날씨는  Clouds 입니다.
    현재온도는 267.81 입니다.
    하지만 체감온도는 260.81 입니다.
    


```python
# 실습
# 최저 기온 : main - temp_min
print('최저 기온은', data['main']['temp_min'],'입니다.' )

# 최고 기온 : main - temp_max
print('최고 기온은', data['main']['temp_max'],'입니다.' )

# 습도 : main - humidity
print('습도는', data['main']['humidity'],'입니다.' )

# 기압 : main - pressure
print('기압은', data['main']['pressure'],'입니다.' )

# 풍향 : wind - deg
print('풍향은', data['wind']['deg'],'입니다.' )

# 풍속 : wind - speed
print('풍속은', data['wind']['speed'],'입니다.' )

```

    최저 기온은 266.84 입니다.
    최고 기온은 267.81 입니다.
    습도는 73 입니다.
    기압은 1010 입니다.
    풍향은 306 입니다.
    풍속은 6.9 입니다.
    

- 언어 및 단위 변경하기 


```python
import requests
import json

city = "Seoul"
apikey = 60c7ab245b89899ec83dd8acbdf5b8f2
lang = "kr"

# units - metric
api = f"""http://api.openweathermap.org/data/2.5/\
weather?q={city}&appid={apikey}&lang={lang}&units=metric""" 

result = requests.get(api)
# print(result.text)

data = json.loads(result.text)
```


```python
# 지역 : name
print(data["name"],"의 날씨입니다.")
# 자세한 날씨 : weather - description
print("날씨는 ",data["weather"][0]["description"],"입니다.")
# 현재 온도 : main - temp
print("현재 온도는 ",data["main"]["temp"],"입니다.")
# 체감 온도 : main - feels_like
print("하지만 체감 온도는 ",data["main"]["feels_like"],"입니다.")
# 최저 기온 : main - temp_min
print("최저 기온은 ",data["main"]["temp_min"],"입니다.")
# 최고 기온 : main - temp_max
print("최고 기온은 ",data["main"]["temp_max"],"입니다.")
# 습도 : main - humidity
print("습도는 ",data["main"]["humidity"],"입니다.")
# 기압 : main - pressure
print("기압은 ",data["main"]["pressure"],"입니다.")
# 풍향 : wind - deg
print("풍향은 ",data["wind"]["deg"],"입니다.")
# 풍속 : wind - speed
print("풍속은 ",data["wind"]["speed"],"입니다.")
```

    Seoul 의 날씨입니다.
    날씨는  구름조금 입니다.
    현재 온도는  -6.11 입니다.
    하지만 체감 온도는  -13.11 입니다.
    최저 기온은  -6.31 입니다.
    최고 기온은  -5.34 입니다.
    습도는  51 입니다.
    기압은  1010 입니다.
    풍향은  300 입니다.
    풍속은  6.17 입니다.
    

### googletrans를 활용한 번역기 만들기 

    1. 번역기 만들기.
    2. 언어 감지를 원하는 문장을 설정한다. 
    3. 언어를 감지한다.


```python
from googletrans import Translator

translator = Translator()

# sentence = "안녕하세요 코드라이언입니다."
sentence = input("번역을 원하는 문장을 입력해주세요 : ")

result = translator.translate(sentence,'english')
detected = translator.detect(sentence)

print("===========출 력 결 과===========")
print(detected.lang,":",sentence)
print(result.dest,":",result.text)
print("=================================")
```

    번역을 원하는 문장을 입력해주세요 : 안녕하세요
    ===========출 력 결 과===========
    ko : 안녕하세요
    en : hello
    =================================
    

### python으로 메일 보내기
    SMTP(Simple Mail Transfer Protocol) : 간단하게 메일을 보내기 위한 약속 
    우리는 smtp서버를 이용해서 원하는 곳으로 메일을 보낼 수 있다. 


```python
import smtplib
from email.message import EmailMessage

#smtp 메일 서버 연결하기 
SMTP_SERVER = "smtp.gmail.com"
SMTP_PORT = 465


# smtp  메일 서버로 메일을 보내기

message = EmailMessage()
message.set_content('코드라이언 수업중입니다.') # 이메일 내용 

message["Subject"] = "이 메일은 python으로 보낸 메일입니다." # 제목
message["From"] = "minchan-work@likelion.org" # 발신자
message["To"] = "qusalscks@gmail.com" # 수신자 



smtp = smtplib.SMTP_SSL(SMTP_SERVER,SMTP_PORT)
print('-------------서버 연결 완료---------------')

# smtp 메일 서버에 로그인 하기
smtp.login('minchan-work@likelion.org','alscks135!')
print('-------------메일 로그인 성공--------------')

# 메세지 보내기 
smtp.send_message(message) 
print('-------------메일 발송 성공--------------')

smtp.quit() # 서버 종료 
print('-------------서버 종료--------------')

```

    -------------서버 연결 완료---------------
    -------------메일 로그인 성공--------------
    -------------메일 발송 성공--------------
    -------------서버 종료--------------
    

#### 사진을 첨부해서 메일 보내기 
    r : read / w : write / a: append
    rb : read binary / wb : write binary/ ab: append binary   
         -> 컴퓨터가 처리하기 쉽도록 이미지를 이해하는 방식
    
    - add_attachment(...) : multipart/mixed 타입의 메일을 보내기 위한 기능 


```python
import imghdr

message_img = EmailMessage()
message_img.set_content('코드라이언 수업중입니다. 사진을 첨부하는 코드를 짜고 있습니다. ') # 이메일 내용 

message_img["Subject"] = "[사진 첨부]이 메일은 python으로 보낸 메일입니다." # 제목
message_img["From"] = "minchan-work@likelion.org" # 발신자
message_img["To"] = "qusalscks@gmail.com" # 수신자 

# 이미지 파일 불러오기 
with open('codelion.PNG',"rb") as image:
    image_file = image.read()

image_type = imghdr.what('codelion.PNG', image_file) # 확장자 자동으로 파악
# print(image_type)

# 이미지 파일 메일에 추가 
message_img.add_attachment(image_file, maintype='image', subtype=image_type)


smtp = smtplib.SMTP_SSL(SMTP_SERVER,SMTP_PORT)
print('-------------서버 연결 완료---------------')

# smtp 메일 서버에 로그인 하기
smtp.login('minchan-work@likelion.org','*******')
print('-------------메일 로그인 성공--------------')

# 메세지 보내기 
smtp.send_message(message_img) 
print('-------------메일 발송 성공--------------')

smtp.quit() # 서버 종료 
print('-------------서버 종료--------------')

```

    -------------서버 연결 완료---------------
    -------------메일 로그인 성공--------------
    -------------메일 발송 성공--------------
    -------------서버 종료--------------
    

### 유효성 검사하기 (정규식)
    정규표현식을 활용해 유효한 이메일 형식만을 보내기


```python
# 소문자 a-z 대문자 A-Z : 2~3번 반복

import re
reg = "^[a-zA-Z0-9.+_-]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,3}$"
print(re.match(reg,"codelion.example@gmail.com"))
```

    <re.Match object; span=(0, 26), match='codelion.example@gmail.com'>
    


```python
import smtplib
from email.message import EmailMessage
import imghdr
import re


# 유효성 검사 함수
def sendEmail(addr):
    reg = "^[a-zA-Z0-9.+_-]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,3}$"
    if bool(re.match(reg,addr)):
        smtp.send_message(message)
        print("정상적으로 메일이 발송되었습니다.")
    else:
        print("유효한 이메일 주소가 아닙니다.")


message_img = EmailMessage()
message_img.set_content('코드라이언 수업중입니다. 사진을 첨부하는 코드를 짜고 있습니다. 본 메일은 유효성 검사가 완료된 메일입니다. ') # 이메일 내용 

message_img["Subject"] = "[사진 첨부]본 메일은 python으로 보낸 메일입니다." # 제목
message_img["From"] = "minchan-work@likelion.org" # 발신자
message_img["To"] = "qusalscks@gmail.com" # 수신자 

# 이미지 파일 불러오기 
with open('codelion.PNG',"rb") as image:
    image_file = image.read()

image_type = imghdr.what('codelion.PNG', image_file) # 확장자 자동으로 파악
# print(image_type)

# 이미지 파일 메일에 추가 
message_img.add_attachment(image_file, maintype='image', subtype=image_type)


# 서버 연결
smtp = smtplib.SMTP_SSL(SMTP_SERVER,SMTP_PORT)
print('-------------서버 연결 완료---------------')

# smtp 메일 서버에 로그인 하기
smtp.login('minchan-work@likelion.org','*******')
print('-------------메일 로그인 성공--------------')


# 메일을 보내는 sendEmail 함수를 호출해서 메시지 보내기 
sendEmail("qusalscks@gmail.com")


smtp.quit() # 서버 종료 
print('-------------서버 종료--------------')
```

    -------------서버 연결 완료---------------
    -------------메일 로그인 성공--------------
    정상적으로 메일이 발송되었습니다.
    -------------서버 종료--------------
    
