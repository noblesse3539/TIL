## 1.  단축평가의 활용

코드의 가독성이 떨어지므로 잘 사용하진 않지만 단축평가를 이용하여 코드의 라인 수를 줄일 수 있다.

``` python
def defduplicated(alphabets):
    ch_list = []
    result = set()
    for x in alphabets:
        if alphabets.count(x) > 1:
            if x not in result:
            	result.add(x)
                ch_list.append(x)
    return ch_list
```

위와 같은 코드를 단축평가와 List Comprehention을 이용하면 아래와 같이 나타낼 수 있다.

```python
def duplicated(alphabets):
    result = set()
    return [x for x in alphabets if alphabets.count(x) >1 and not (x in result or result.add(x))]
```



## 2. 딕셔너리 메소드 활용

1) pop(keyp, default])

​	key가 딕셔너리에 있으면 제거하고 그 값을 돌려준다. 그렇지 않으면 default를 반환한다.

``` python
my_dict = {'apple': '사과'}
my_dict.pop('apple')
```

> '사과'

​	이후에 my_dict.pop('apple')을 수행 할 경우 `KeyError`를 띄운다.

``` python
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-3-2a8b4f967f4a> in <module>
----> 1 my_dict.pop('apple')

KeyError: 'apple'
```

default를 설정할 경우 딕셔너리에 키가 없더라도 정해진 값을 리턴시킬 수 있다.

``` python
my_dict.pop('apple', 0)
```

> 0



2) .update()

​	값을 제공하는 key, value로 덮어쓴다.

``` python
my_dict.update({'pineapple':'파인애플'})
print(my_dict)
```

​	my_dict에 파인애플이 추가된다.

3) .get(key[, default])

​	key를 통해 value를 가져오며, 없을 경우 default 값을 반환한다.

​	절대로 KeyError가 발생하지 않는다. 

``` python
my_dict = dict()
my_dict.get('grape')
```

\> -100

### 2.1 dictionary comprehension

리스트 컴프리헨션처럼 딕셔너리도 딕셔너리 컴프리헨션을 통해 코드를 간결화 할 수 있다.

ex)

```  python
# 숫자와 세제곱의 결과로 이뤄진 딕셔너리를 만들어봅시다.
cubic = {x: x**3 for x in range(1, 10)}
print(cubic)
```

> {1: 1, 2: 8, 3: 27, 4: 64, 5: 125, 6: 216, 7: 343, 8: 512, 9: 729}



## 자주 사용하는 함수들!!

1. map(function, iterable) : 반복가능한 객체의 모든 원소에 function을 적용하여 반환한다.
2. zip(*iterable) : 반복 가능한 여러 객체들의 각 원소들을 하나의 튜플로 묶어  반환해준다.
3. filter(function, iterable) : 반복 가능한 객체의 모든 원소에 `bool 값을 반환하는 함수`를 적용시켜 `True`가 나온 원소들만 추려 반환한다.



ex )

* map()

``` python
a = [1, 2, 3]
list(map(str, a))
```

> ['1', '2', '3']

* zip() - (주의! 길이가 가장 짧은 객체를 기준으로 값을 묶어 반환한다.)

``` python
a = ['a','b','c']
b = [1, 2, 3, 4]
list(zip(a, b))
```

> [('a', 1), ('b', 2), ('c', 3)]

* filter()

```python
# 짝수인지 판단하는 함수
def even(n):
    if n%2:
        return False
    else:
        return True
```

```python
a = [1, 2, 3, 4]
list(filter(even, a))
```

> [2, 4]



## 3. 세트 메소드 활용

1) .add(elem) : elem을 세트에 추가한다.

2) .update(*others) : 여러가지의 값을 순차적으로 추가한다.

3) .remove(elem) : elem을 세트에서 삭제한다. 없을경우 KeyError가 발생!!

4) .deiscard(elem) : elem을 세트에서 삭제한다. 없어도 에러가 발생하지 않는다.

5) .pop(): 세트에서 임의의 원소를 제거해 반환한다. 만약 세트가 비어있을 경우 KeyError 발생!!

