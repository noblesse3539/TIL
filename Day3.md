# Day3

## 1. Dictionary

Dictionary는 `key`와 `value`가 짝지어져있다.

key는 `string`, `integer`, `boolean`이 가능하다. `list` 혹은 `dictionary`는 안된다.

value는 모든 자료형이 가능하다. `list` 혹은 `dictionary`도 가능하다.

1) 딕셔너리 만들기

```python
phonebook = {
    "중국집" : "031-123-1234"
}
phonebook2 = dict(중국집=031-123-1234)
```

2) 딕셔너리 조작하기

```python
phonebook["분식집"] = "031"
```

3) 딕셔너리 내용 가져오기

```python
idol = {
    "bts" : {
        "지민" : 23,
        "RM" : 25
    }
}
# 랩몬스터의 나이는?
idol["bts"]["RM"]
```

4) 딕셔너리 반복문 활용하기

```python
# 기본 활용
for key in phonebook:
    print(key)
    print(phonebook[key])
    
# .items()
for key, value in phonebook.items():
    print(key, value)
    
# .values()
for value in phonebook.values():
    print(value)

# .keys()
for key in phoebook.keys():
    print(key)
```



### [연습문제](https://zzu.li/dj_dict1)

```python
score = {
    "iu": {
        "수학": 80,
        "국어": 90,
        "음악": 100
    },
    "ui": {
        "수학": 80,
        "국어": 90,
        "음악": 100
    }
}

# 풀이
sumOfScore = 0
numOfScore = 0
for dict in score.values():
    for value in dict.values():
        sumOfScore += value
        numOfScore += 1

print(sumOfScore/numOfScore)
```

## 2.텔레그램 API 활용하기

> 사전 준비사항: @botfather를 통해서 봇을 만들어서 토큰 정보를 기록한다.

### 0)봇 정보 가져오기

```python
https://api.telegram.org/bot{token}/getME
```

```python
import requests
token = "토큰"
url = f"https://api.telegram.org/bot{token}/getME"
response = requests.get(url)
```

### 1) 메세지 보내기

(1) user의 `id`를 가져와야함.

```python
https://api.telegram.org/bot{token}/getUpdates
```

```python
import requests
token = "토큰"
url = f"https://api.telegram.org/bot{token}/getUpdates"
response = requests.get(url).json()
currentResult = len(updates["result"])-1 # 메세지를 보낼 때마다 추가됨.
user_id = response["result"][currentResult]["message"]["from"]["id"]
msg = "안녕?"

send_url = f"https://api.telegram.org/bot{token}/sendMessage?text={msg}&chat_id={user_id}"
requests.get(send_url)
```



