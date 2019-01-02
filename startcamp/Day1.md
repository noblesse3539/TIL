# Day1

## 1. CLI(command Line Interface)

명령어를 통해서 사용하는 인터페이스로, GUI(Graphic User Interface)와는 다르게 터미널(bash/shell/cmd)을 통해서 명령을 할 수 있다.

사전 준비사항 : [Git bash](https://gitforwindows.org) 설치

### 1. 기본 명령어

```
$ ls
```

## 2. Python

### 0) Python Style Guide(PEP-8)

​	[공식문서 링크](https://www.python.org/dev/peps/pep-0008)

### 1) string 조작


```python
# 기본 방법
print("안녕하세요")
print("저는 홍길동입니다.")
print("만나서 반갑습니다.")

print("""안녕하세요
저는 홍길동입니다.
만나서 반갑습니다.
""")
```

출력결과:

```
안녕하세요
저는 홍길동입니다.
만나서 반갑습니다.

안녕하세요
저는 홍길동입니다.
만나서 반갑습니다.
```



#### (2) String Interpolation

1. f-string

   ```python
   name = "홍길동"
   print(f"안녕하세요, {name}입니다.")
   #=> "안녕하세요, 홍길동입니다."
   ```

2.  [pyformat](https://pyformat.info/)

   ```python
   name = "홍길동"
   english_name = "hong"
   print("안녕하세요, {}입니다. My name is {}.".format(name, english_name))
   #=> "안녕하세요, 홍길동입니다. My name is hong.
   print("안녕하세요, {1}입니다. My name is {0}.".format(name, english_name))
   #=> "안녕하세요, hong입니다. My name is 홍길동.
   print("안녕하세요, {1}입니다. My name is {1}.".format(name, english_name))
   #=> "안녕하세요, hong입니다. My name is hong.
   ```


3. 모르면 이렇게 하자

   ```python
   name = "홍길동"
   print("안녕하세요, " + name + "입니다.")
   #=> 안녕하세요 홍길동입니다.
   ```


### 2) range

`range`는 숫자의 범위를 가지고 있는 시퀀스다.

```python
print(range(5))
#=> range(0,5)
# list 형변환
a = list(rane(5))
print(a)
#=> [0,1,2,3,4]

# 반복문 활용
for i in range(3):
    print(i)
#=> 0
#=> 1
#=> 2
```



### 3) List

`list`는 배열 또는 array라고도 불린다. 인덱스를 통해 값에 접근할 수 있다.

```python
menu = ["중국집", "초밥", "고기", "분식"]
menu[0]
#=> 중국집
```

`list`는 정렬을 할 수 있다.

```python
a = [3,1,2]
# 1. sorted
sorted(a)
#=> [1,2,3] 리턴
print(a)
#=> [3,1,2]
a = sorted(a)
print(a)
#=> [1,2,3]

# 2. .sort()
a.sort()
#=> None 리턴
print(a)
#=> [1,2,3]
```





### 4) Dictionary

`Dictionary`는 hash(해쉬)라고도 불린다. `key`와 `value`가 짝지어져 있다.

```python
phonebook = {
    "중국집" : "123-1234",
   	"초밥" : "456-4567",
    "고기" : "789-7890", 
    "분식" : "012-0123"
}
phonebook["중국집"]
#=> 123-1234
```



## 3. [마크다운(Markdown)](https://www.markdownguide.org/)

### 1. Heading

```
# H1입니다.
## H2입니다.
### H3입니다.
#### H4입니다.
##### H5입니다.
```

# H1입니다.
## H2입니다.
### H3입니다.
#### H4입니다.
##### H5입니다.



### 2.List

```
* 순서 없는 리스트
* 순서 없는 리스트

1. 순서 있는 리스트1
2. 순서 있는 리스트2
3. 순서 있는 리스트3
```

* 순서 없는 리스트
* 순서 없는 리스트

1. 순서 있는 리스트1
2. 순서 있는 리스트2
3. 순서 있는 리스트3



### 3. 코드 작성(Code snippet)

```
​```python
print("hello, world")
​```
```

```python
print("hello, world")
```



### 4. 링크 연결

```
[구글로 가는 링크](https://google.com)
```

[구글로 가는 링크](https://google.com)



### 5. 글씨 꾸미기

```
_기울임_
*기울임*
**굵게**
__굵게__
**_굵게기울임_**
<u>밑줄</u>
```

*기울임*

**굵게**

**_굵게기울임_**

<u>밑줄</u>



### 6. 기타

```
---
***
> 안녕하세요?
인용문 공간입니다.
```

---

***

> 안녕하세요?
>
> 인용문 공간입니다.

