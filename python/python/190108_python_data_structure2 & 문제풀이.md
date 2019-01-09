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