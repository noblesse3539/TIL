# React Native

## 1. 인스톨

``` bash
$ npm install expo-cli --global
```



## 2-1. 프로젝트 생성

* 깃배쉬에서는 설정이 잘 이루어지지 않으므로 cmd에서 입력하자. 선택지가 나온다.

``` bash
$ expo init my-new-project
$ cd my-new-project
$ yarn start (혹은 expo start)
```

* qr 코드가 생성되고 단말기에서 expo앱을 실행후 qr코드를 찍으면 연동된다.
* 설치 완료 후, 단말기를 흔들면 expo 설정탭을 볼 수 있다.
* [코딩 스타일 설정방법](https://velopert.com/3671)



## 3. 설정탭 주요기능

1. Live Reload : 코드 작성후 저장하면 자동으로 리로드 한다.
2. Hot Reloading : 코드의 변경된 부분만 새로고침한다!!!! 겁나 중요!!!



## 4. 특징

* React Native는 컴포넌트를 반환하는 것에서 react 와 같지만, 사용하는 컴포넌트가 다르다. 실제로 div, h1 과 같은 태그는 사용할 수 없고 react native에서 제공되는 컴포넌트로만 구성할 수 있다.
* 컴포넌트의 위치를 flex-box로 변환할 수 있다!!
* 굉장히 엄격하다. html이나 css등에 오타가 있어도 web은 정상적으로 작동하지만, react native의 경우 빨간화면이 바로 나타나면서 잘못된 부분을 알려준다. react native만의 명확한 규칙과 패턴을 익히자.



## 5. Flexbox

* flex direction의 디폴트가 column이다. (html, css에서 flex direction의 디폴트는 row이다.)

* justify-content 같은 경우 캐멀케이스를 사용해 `justifyContent`처럼 작성하고, 속성값은 문자열로 넣는다.

* ``` jsx
  ...
  	<View style={styles.container}>
  ...
  
  
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      backgroundColor: '#fff',
      flexDirection: 'row',
      justifyContent:'flex-start',
      alignItems:'flex-end',
      flexWrap:'wrap'
    },
  ```



## 6. 코드 요령

아래의 코드에서 state의 isLoaded의 값에 따라 호출하는 값을 변형시킨다. react에서 state는 유동적인 값을 설정할 때 사용한다.

``` jsx
export default class App extends React.Component {
  state = {
    isLoaded: false
  }
  render() {
    const { isLoaded } = this.state;
    return (
      <View style={styles.container}>
        {isLoaded ? null : (
          <View style={styles.loading}>
            <Text style={styles.loadingText}>Getting the weater</Text>
          </View>
        )}
      </View>
    );
  }
}
```



## 7. 다양한 패키지

react native와 expo 사이트의 docs를 살펴보면서 필요한 요소들을 사용하자.

```jsx
import { StyleSheet, Text, View } from 'react-native';
import {LinearGradient} from 'expo';
```



[vector-icons](https://expo.github.io/vector-icons/) : expo는 font awesome을 비롯한 다양한 아이콘을 사용할 수있는 라이브러리가 존재한다. 이름, 크기, 색상만 지정하여 아이콘을 간단하게 사용할 수 있다.

``` jsx
import { Ionicons } from '@expo/vector-icons';
...
	<Ionicons name="ios-rainy" size={144} color="white" />
...
```

## 8. 위치 확인

자바스크립트에서 현재의 위치를 확인하는 방법은 아래와 같다. react native에서도 동일한 방법으로 위치정보를 가져올 수 있다.

``` javascript
navigator.geolocation.getCurrentPosition(function(position) {
    console.log(position)
})
```

