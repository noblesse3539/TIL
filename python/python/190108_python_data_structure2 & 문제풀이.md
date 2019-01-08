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

