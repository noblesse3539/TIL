#  1 문자열 메소드 활용하기

## strip([chars]) : 글씨 제거

특정한 문자를 지정하면, 양쪽을 제거하거나 왼쪽, 오른쪽을 제거한다. 지정하지 않으면 공백을 제거한다.

``` python
'     wow!     '.strip()
```

> 'wow!'

``` python
'     wow!     '.lstrip()
```
> 'wow!     '
``` python
'     wow!     '.rstrip()
```
> '      wow!'

```python
'hihihihihiihihihihi'.strip('hi')
```

> ''

 ```python
'a_a_a'.strip('a')
 ```

> '\_a\_'



## .find(x) 와 .index(x)의 차이

둘 다 x가 위치한 첫번째 인덱스를 반환하지만,

.find(x) : 없을 경우 -1을 리턴

.index(x) : 없을 경우 에러 



### .isdecimal() : ex) '123'.isdecimal() / 해당 문자열이 10진수인지 판별



## split()

문자열을 특정한 단위로 나누어 리스트로 반환

``` python
inputs = input().split()
print(inputs)
```

> \>5 3 1 2 5
>
> [5', '3', '1', '2', '5']



## !!! 문자열 뒤집기 !!!

### 1)

``` python
'123'[::-1]
```

> \> '321'

### 2)

``` python
''.join(reversed('123'))
```

> \> '321'



# 2 리스트 메소드 활용하기

## 1)추가

* .append(x) : 리스트 위에 값 추가
* .extend(iterable) : 리스트에 리스트, 튜플 등을 추가할 때 사용
* .insert(i, x) : 특정 위치에 삽입할 때 사용



## 2) 삭제

* .remove(x) : 값이 x인 것을  삭제
* .pop(i) : i 인덱스에 있는 값을 삭제하며, 그 항목을 반환함



## 3) 탐색 및 정렬

* .index(x) : 원하는 값을 찾아 첫번째 index를 반환
* .count(x) : x의 갯수를 반환



* .sort() : 원본 list를 변형시키고, None을 리턴 ( sorted()와 혼동 X )
* .reverse() : 반대로 뒤집는다. ( 정렬이 아님)



# 3 복사

리스트의 값 복사는 다음과 같이 할 수 있다.

### 1)

``` python
a = [1, 2, 3]
b = a[:]
print(id(a), id(b))
```

> 1825519172104 1825519133832



### 2)

``` python
a = [1, 2, 3]
b = list(a)
b[0] = 5
print(a)
```

> [1, 2, 3]



### 3)

``` python
import copy
a = [1, 2, 3]
b = copy.copy(a)
b[0] = 5
print(a)
```

> [1, 2, 3]



위의 케이스는 모두 얕은 복사이다. 얕은 복사에서는 다중리스트를 복제할 경우 참조를 하기 때문에 주의해야 한다.

[얕은 복사](https://goo.gl/ZH6yZd) VS [깊은 복사](https://goo.gl/FZcYbJ)

### 4) 깊은 복사

``` python
import copy
a = [[1, 2], 2, 3]
b = copy.deepcopy(a)
b[0][0] = 5
print(a)
```

> [[1, 2], 2, 3]



## 4 삭제

* .clear() : 리스트의 모든 항목을 삭제



## List Comprehension

* List를 만들 수 있는 간단한 방법!! 아주 중요한 방법
* for문이나 if문을 중첩적으로 사용 가능하다.

사용법 :

``` python
even_list = [x for x in range(1, 11) if x % 2 == 0]
print(even_list)
```

> [2, 4, 6, 8, 10]

```python
girls = ['jane', 'iu', 'mary']
boys = ['justin', 'david', 'kim']
a = [(j, i) for i in girls for j in boys]
print(a)
```

>  [('justin', 'jane'), ('david', 'jane'), ('kim', 'jane'), ('justin', 'iu'), ('david', 'iu'), ('kim', 'iu'), ('justin', 'mary'), ('david', 'mary'), ('kim', 'mary')]

``` python
words = 'Life is too short, you need python!'
vowel = 'aeiou'
result = [x for x in words if x not in vowel]
print(''.join(result))
```

> Lf s t shrt, y nd pythn!

