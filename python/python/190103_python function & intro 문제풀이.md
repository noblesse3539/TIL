# python function & intro 문제풀이



## intro 문제 풀이

### split(str) 

해당 문자열을 인자로 준 문자가 나올 경우 끊어서 list 형태로 반환해준다.

``` python
name = 'Alice Betty Catherine Davis'
name_split = name.split(' ')
print(name_split)
```

> ['Alice', 'Betty', 'Catherine', 'Davis']



### .join(list)

`list` 의 각 `str` 요소를 지정한 문자열로 엮고 하나의 문자열로 합쳐서 반환해준다. int 는 안됨.

``` python
l = [1,2,3,4,5]
l = list(map(str, l))
a = '-'.join(l)
print(a)
```

> 1-2-3-4-5



### fstring 확장

1. <: 왼쪽 정렬
2. ^: 가운데 정렬
3. \>: 오른쪽 정렬

``` python
greeting = '안녕하세요'
print(f'{greeting:<10}')
print(f'{greeting:^10}')
print(f'{greeting:>10}')
```

> ```
> 안녕하세요     
>   안녕하세요   
>      안녕하세요
> ```



## python function

* 함수는 코드의 간결화, 유지 보수를 위해 사용한다.
* 코드가 많아질 수록 문제가 발생할 확률이 높아지며, 유지 보수하기도 힘들어진다.



### 함수 기본 형태

``` python
def rectangle(height, width):
    area = height * width
    perimeter = 2 * (height + width)
    print(area, perimeter)
```



### return

오직 한 개의 객체만 반환한다. 여러 개를 반환할 경우, 하나의 `tuple`을 반환한다.



### 기본 값(Default Argument Values)

* 함수가 호출될 때, 인자를 지정하지 않아도 기본 값을 설정할 수 있다.

``` python
def greeting(name ='익명'):
    print(f'안녕, {name}아')
greeting()
```

> 안녕, 익명아



* 단, 기본 매개변수 이후에 기본 값이 없는 매개변수를 사용할 수는 없다.

``` python
def greeting(name='성민', age):
    print(f'{age}, {name}')
```

```python
  File "<ipython-input-44-66e60d88aa4a>", line 2
    def greeting(name='성민', age):
                ^
SyntaxError: non-default argument follows default argument
```



### 키워드 인자(Keyword Arguments)

* 키워드 인자는 직접적으로 변수의 이름으로 특정 인자를 전달할 수 있다.

``` python
# 키워드 인자 예시
def greeting(age, name='ssafy'):
    print(f'{name}은 {age}살입니다.')
greeting(name='opalcat', age = 3)
```

> opalcat은 3살입니다.

* 키워드 인자를 활용한 뒤에 위치 인자를 활용할 수는 없다.

``` python
greeting(age=24, '철수')
```

```python
  File "<ipython-input-46-4d90a4f964ea>", line 2
    greeting(age=24, '철수')
                    ^
SyntaxError: positional argument follows keyword argument
```



### 가변 인자 리스트

* 정해지지 않은 임의의 숫자의 인자를 받기 위해 가변인자를 활용할 수 있다.
* 가변인자는 `tuple` 형태로 처리가 되며, `*` 로 표현한다.

**활용법**

```python
def func(*args):
```

``` python
print('hi', '안녕', '할로', '구텐탁', sep='-')
```

> hi-안녕-할로-구텐탁



### 정의되지 않은 인자들 처리하기

* 정의되지 않은 인자들은 `dict` 형태로 처리가 되며, `**` 로 표현한다.
* 주로 `kwagrs` 라는 이름을 사용하며, `**kwargs` 를 통해 인자를 받아 처리할 수 있다.

**활용법**

```python
def func(**kwargs):
```

#### dictionary를 인자로 넘기기

``` python
def my_url(itemPerPage=10, **args):
    base_url = 'http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?'
    base_url += f'itemPerPage={itemPerPage}&'
    for key, value in args.items():
        base_url += f'{key}={value}&'
    return base_url

```
```python
api = {
    'key': 'abc',
    'tagetDt': 'yyyymmdd'
}
my_url(**api)
```
> http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?itemPerPage=10&key=abc&targetDt=yyyymmdd&



### 이름공간 및 스코프(Scope)

* 파이썬에서 사용되는 이름들은 이름공간(namespace)에 저장되어 있다.
* LEGB Rule을 따른다

#### LEGB Rule

>- L`ocal scope: 정의된 함수
>- `E`nclosed scope: 상위 함수
>- `G`lobal scope: 함수 밖의 변수 혹은 import된 모듈
>- `B`uilt-in scope: 파이썬안에 내장되어 있는 함수 또는 속성

* 이름공간은 각자의 수명주기가 있다.

> - built-in scope : 파이썬이 실행된 이후부터 끝까지
> - Global scope : 모듈이 호출된 시점 이후 혹은 이름 선언된 이후부터 끝까지
> - Local/Enclosed scope : 함수가 실행된 시점 이후부터 리턴할때 까지



