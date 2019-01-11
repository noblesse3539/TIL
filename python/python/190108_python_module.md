# 모듈 활용

표준 라이브러리에서 제공되는 모듈을 사용하기 위해서 import를 사용한다.

없는 경우 pip install을 해준 후 import를 한다.

``` python
import random

from bs4 import BeautifulSoup
```



### 난수 발생관련 함수 (random)

``` python
numbers = range(1, 46)
random.sample(numbers, 6) # numbers 중 6개를 반환함
random.choice(numbers) # numbers 중 하나를 반환
random.random() # 난수를 생성함 ex ) 0.5390545851081353
random.randint(1, 5) # [1~5] 중 임의의 정수를 반환한다.
random.seed(1) # 시드를 설정하면 항상 같은 값부터 시작한다.

a = ['kim', 'kang', 'yu', 'choi', 'hwang']
random.shuffle(a)
print(a)
#['kang', 'kim', 'hwang', 'yu', 'choi']
# 시퀀스 객체를 섞는다.
```



### 날짜 관련 모듈

1. datetime

```python
import datetime

now = datetime.datetime.now() # 지금 시간을 반환
datetime.datetime.today() # 오늘을 출력하는 다른 방법
datetime.datetime.utcnow() # UTC기준시를 반환 
```



- 시간 형식지정

| 형식 지시자(directive) | 의미                   |
| ---------------------- | ---------------------- |
| %y                     | 연도표기(00~99)        |
| %Y                     | 연도표기(전체)         |
| %b                     | 월 이름(축약)          |
| %B                     | 월 이름(전체)          |
| %m                     | 월 숫자(01~12)         |
| %d                     | 일(01~31)              |
| %H                     | 24시간 기준(00~23)     |
| %I                     | 12시간 기준(01~12)     |
| %M                     | 분(00~59)              |
| %S                     | 초(00~61)              |
| %p                     | 오전/오후              |
| %a                     | 요일(축약)             |
| %A                     | 요일(전체)             |
| %w                     | 요일(숫자 : 일요일(0)) |
| %j                     | 1월 1일부터 누적 날짜  |

``` python
now.strftime('%Y %M %d %h:%M')
```

\> '2019 29 08 Jan:29'

| 속성/메소드 | 내용                 |
| ----------- | -------------------- |
| .year       | 년                   |
| .month      | 월                   |
| .day        | 일                   |
| .hour       | 시                   |
| .minute     | 분                   |
| .second     | 초                   |
| .weekday()  | 월요일을 0부터 6까지 |

``` python
f'{now.year}년 {ow.month}월 {now.day}일'
```

\> 2019년 1월 8일'

