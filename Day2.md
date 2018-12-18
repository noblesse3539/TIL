# Day2



## 1. 파이썬 쉘 명령어

1) exit() : 파이썬 쉘을 빠져나온다.

```
>>> exit()
```



## 2. import webbrowser

### 1) webbrowser.open(url)

​	해당 url을 브라우저(크롬, 익스플로러 등)로 열어준다.

``` python
import webbrowser
webbrowser.open("https://google.com")
#=> true
```

### 2) 응용

f_string으로 3개의 창을 차례로 띄우기


```python
import webbrowser
starList = ['콜드플레이', '아이유', '검정치마']
url = "https://google.com/search?q="
for i in starList:
    webbrowser.open(f"{url}{i}")
```



## 2. 스크래핑 기초

### 1. 설치

`pip`는 파이썬으로 작성된 패키지 소프트웨어를 설치, 관리하는 패키지 관리 시스템이다.

bash에서 아래와 같이 입력하여 필요한 패키지를 다운받는다.

```
$ pip install requests
$ pip install bs4
```

* `requests` : 요청을 대신 보내준다. [`requests 공식 문서`](http://docs.python-requests.org/en/master/)
* `bs4` : 문서를 파싱하는 것을 도와준다.

### 2_1.  코스피 지수 가져오기

1. 네이버에서 증권 피이지를 요청한다.
2. 페이지에서 내가 찾고 싶은 내용을 찾는다.

```python
import requests
from bs4 import BeautifulSoup
url = "https://finance.naver.com/sise/"
# 1. 원하는 사이트에 요청을 보낸다.
# 그리고, 그 결과를 저장한다.
response = requests.get(url)
	#print(type(response))
	#print(response.text)

# 2. 원하는 정보를 찾는다.
soup = BeautifulSoup(response.text, 'html.parser')
# 3. select는 CSS의 선택자(selector)를 통해 찾을 수 있다.
# #KOSPI_now : id가 KOSPI_now인 것.
# .up : class가 up인 것.
# CSS에서 id는 문서에서 하나, class는 여러개가 있을 수 있다.
kospi = soup.select_one('#KOSPI_now')
print(kospi.text)

```

`BeautifulSoup()`사용 시 웹의 내용을 `string`이 아닌 `bs4.BeautifulSoup` 객체로 가져온다.

`select()` : 결과물을 list의 형태로 가져온다.  

`select_one()` : 결과물 중 가장 앞에 있는 하나만 가져온다.

#### select()

``` python
select('#a') # id가 a인 것을 가져온다.
select('.a') # class가 a 인 것을 가져온다.
```

### 2_2. 실시간 검색어 가져오기

```python
import requests
from bs4 import BeautifulSoup
url = "https://naver.com/"
# 1. 원하는 사이트에 요청을 보낸다.
# 그리고, 그 결과를 저장한다.
response = requests.get(url)
#print(type(response))
#print(response.text)

# 2. 원하는 정보를 찾는다.
soup = BeautifulSoup(response.text, 'html.parser')
realtime = soup.select(".ah_roll") #class가 ah_roll인 것
sets = realtime[0].select(".ah_k") #class가 ah_k인 것
for word in sets:
    print(word.text)
```

## 3. HTML/CSS

### 1. HTML

HTML은 HyperText Markup Language의 약자로, 웹 문서에서 활용이 된다.

웹 문서의 구조와 내용을 담당한다.

```html
<!Doctype html>
<html>
    <head>
        <!-- 문서의 정보를 담고 있다 -->
        <title>네이버</title>
    </head>
    <body>
        
    </body>
</html>
```

### 2. CSS

CSS는 Cascading Style Sheets의 약자로, HTML과 같은 마크업 언어를 꾸며주는 역할을 한다.

꾸며주기 위해서 특정한 태그를 선택해야하는데 이때 활용되는 것이 `css 선택자(selector)` 라고 부른다.

* id : #
* class : .
* tag

```html
<!Doctype html>
<html>
    <head>
        <style>
            #blue {
                color : blue;
            }
            .red {
                color : red;
            }
            p {
                color: skyblue;
            }
        </style>
    </head>
    <body>
        <p class ="red">클래스 적용</p>
        <p>태그 적용</p>
        <p id ="blue">id 적용</p>
        <p id ="blue" class = "red">파란색</p>
        <p style="color :red">인라인 속성</p>
    </body>
</html>
```

선택자에는 우선순위가 존재한다. `in line` > `id` > `class` > `tag` . inline이 가장 우선순위가 높다.

## 3. 파일 조작

### 1. `os` 외장 함수

```python
import os

os.chdir(r"경로") # 현재 디렉터리를 변경한다.
os.getcwd() # 현재 워킹 디렉터리를 보여준다.
os.listdir() # 현재 디렉터리에 있는 파일들을 보여준다.
os.rename(f, "추가"+f) # f 라는 이름의 파일 명을 변경한다.
```



```python
import os

# SSAFY지원자 폴더로 들어간다.
os.chdir(r"SSAFY지원자")
# SSAFY지원자 폴더로 들어간다.
os.chdir(r"SSAFY지원자")
# 내용 모두 출력
files = os.listdir()
print(files)
for f in files:
    os.rename(f, "지원자_"+f) # 지원자_아무개 로 변경됨.
    os.rename(f, "SAMSUNG"+f) # SAMSUNG지원자_아무개 로 변경됨.
    os.rename(f, f.replace("SAMSUNG", "SSAFY")) # SAMSUNG이 SSAFY로 변경됨.
```

`replace()` : os의 함수가 아닌 내장형 함수이다.

### 2. file 열어서 조작하기

#### 1) 기본 사용법

```python
with open("파일명", "w") as file:
    file.write("글써짐")

with open("파일명", "r") as file:
    line = file.read()
    print(line)
```

파일을 조작하는 모드는 다음과 같다.

* w : write(덮어쓰기)

* r : read(읽기)

* a : append(이어쓰기)


#### 2) 파일 읽기

```python
# 1. read() : 전체를 하나의 string
line = file.read() # 전체 내용

# 2. readline() : 한줄씩 string으로 가져옴.
line = file.readline() # 첫번째 줄
line = file.readline() # 두번째 줄

# 3. readlines() : 전체를 하나의 list, element는 한 줄의 string
lines = file.readlines()
for line in lines:
    print(line)
```

### 번외_ strip()

```python
line = "     asdfasdf     "
print(line.strip()) # 공백 등을 없애준다.
#=> asdfasdf

#응용
line.lstrip()
#=>'asdfasdf     '
line.rstrip()
#=>'      asdfasdf'

```

