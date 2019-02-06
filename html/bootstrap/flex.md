# Flex 

[개구리 조종하기](flexboxfroggy.com)

## 1. justify-content

* flex-start: 요소들을 컨테이너의 왼쪽으로 정렬
* flex-end: 요소들을 컨테이너의 오른쪽으로 정렬
* center: 요소들을 컨테이너의 가운데로 정렬
* space-between: 요소들 사이에 동일한 간격
* space-around: 요소들 주위에 동일한 간격

```css
#pond {
    display: flex;
    justify-content: flex-end;
}
```

## 2. align-items

* flex-start: 요소들을 컨테이너의 꼭대기로 정렬
* flex-end: 요소들을 컨테이너의 바닥으로 정렬
* center: 요소들을 컨테이너의 세로선 상의 가운데로 정렬
* baseline: 요소들을 컨테이너의 시작 위치에 정렬
* stretch: 요소들을 컨테이너에 맞도록 늘림

``` css
#pond {
    display: flex;
    align-items: flex-end
}
```

## 3. flex-direction

* row: 요소들을 텍스트의 방향과 동일하게 정렬
* row-reverse: 요소들을 텍스트의 반대 방향으로 정렬
* column: 요소들을 위에서 아래로 정렬
* column-reverse: 요소들을 아래에서 위로 정렬

``` css
#pond {
    display: flex;
    flex-direction: row-reverse;
}
```

* column-reverse 또는 row-reverse를 사용하면 요소들의 start와 end의 순서도 뒤바뀐다.
* flex의 방향이 column일 경우 justify-content의 방향이 세로로, align-items의 방향이 가로로 바뀐다.



## 4. order

* item들 각각의 순서를 변경할 수 있다.
* 기본값은 0이며, 양수나 음수로 바꿀 수 있다.

``` css
.yellow {
    order: 1;
}
```



## 5. align-self

* align-self : 지정된 align-item 값을 무시하고 Flex 요소를 세로선 상에서 정렬

```css
.yellow {
    align-self: flex-end;
}
```



## 6. flex-wrap

* nowrap: 모든 요소들을 한 줄에 정렬
* wrap: 요소들을 여러 줄에 걸쳐 정렬
* wrap-reverse: 요소들을 여러 줄에 걸쳐 반대로 정렬



## 7. flex-flow
flex-direction과 flex-wrap은 자주 같이 사용되기 때문에, flex-flow가 이를 대신할 수 있다.

``` css
#pond {
    display: flex;
    flex-flow: row wrap
}
```



## 8. align-content

* flex-start: 여러 줄들을 컨테이너의 꼭대기에 정렬
* flex-end: 여러 줄들을 컨테이너의 바닥에 정렬
* center: 여러 줄들을 세로선 상의 가운데에 정렬
* space-between: 여러 줄들 사이에 동일한 간격을 둠
* space-around: 여러 줄들 주위에 동일한 간격을 둠
* stretch: 여러 줄들을 컨테이너에 맞도록 늘림



align-content는 여러줄들 사이의 간격을 지정, align-items는 컨테이너 안에서 어떻게 모든 요소들이 정렬하는지를 지정, 한 줄만 있는 경우, align-content는 효과를 보이지 않는다.

``` css
#pond {
    display: flex;
    align-content: flex-start;
}

```

