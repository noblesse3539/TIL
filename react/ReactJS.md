# ReactJS

## 1. node.js, npx, yarn 설치 (VSCode 편하므로 추가)

​	컴파일이나 reload 속도가 npx보다 yarn이 더 우수하므로 yarn을 사용한다.

## 2. [create-react-app](https://github.com/facebook/create-react-app) | yarn으로 app project 만들기

```bash
$ yarn create react-app <앱 이름>

%서버 구동 방법%
$ cd <앱 이름>
$ yarn start
```

### <만들어진 프로젝트 구조>

```
my-app(앱 이름)
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── serviceWorker.js
```

>  index.js 에서, ReactDOM.render()를 사용해, 
>
>  App.js 의 단 하나의 컴포넌트<App/>를 ,
>
> index.html의 `<div id="root">`로 보낸다.

## 즉, 여러 컴포넌트는 디렉터리 src/ 안에 js 형태로 만들 수 있으며, App 컴포넌트안에 차곡차곡 쌓아올린 후, 최종적으로 App 컴포넌트를 html에 render 시킨다.



## 3. Component의 구조

```jsx
// App.js
import React, { Component } from 'react';
import './App.css'
import Movie from './Movie'
class App extends Component {
    render() {
        return (
        	<div className="App">
                <Movie/> // 얘는 또다른 컴포넌트임
            </div>

        )
    }
}
export default App;

//기본적으로 컴포넌트는 render() 가 필수적으로 존재해야 한다.
```

### 서버 실행 시, 코드가 수정되었을 경우, 자동으로 컴파일하며 브라우저를 새로고침한다.



## 4. props

​	부모 컴포넌트에서 자식 컴포넌트로 데이터를 넘겨주기 위해 사용한다.

* 부모 컴포넌트

```jsx

class App extends Component {
    ...
    render() {
        ...
        
        {this.state.movies.map((movie, index) => {
            // 아래와 같이 인자를 설정하여 넘겨줌, 
            return <Movie title={movie.title} poster={movie.poster} key={index}/>
        })}
    }
   
}
```

* 자식 컴포넌트

```jsx
class Movie extends Component{
	// 부모로부터 받는 요소들의 타입을 제한할 수 있다. 불일치시 에러.
    // 뒤에 isRequired가 있으면 반드시 받아야 함.
    static propTypes = {
        title: PropTypes.string.isRequired,
        poster: PropTypes.string.isRequired
    }
    render() {
        return (
            //{this.props.??}을 사용하여 부모와 데이터를 주고받을 수 있다. 
            <div>
                <MoviePoster poster={this.props.poster}/>
                <h1>{this.props.title}</h1>
            </div>
        )
    }
}
```

[Array.prototype.map() 사용법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

## 5. Render 및 Update 작동 순서

### Render:

1. componentWillMount()  : API에 요청해서 받아오거나 할 때 쓰면 유용
2. render() : 응답받은 데이터를 처리, 반드시 정의되어야 함
3. componentDidMount() : 컴포넌트가 완전히 자리잡았음

### Update:

1. componentWillReceiveProps() 
2. shouldComponentUpdate()
3. componentWillUpdate() : 예시) 이 함수 안에서 어플리케이션에 뱅글뱅글 돌아가는 스피너(로딩중을 나타낼 때)를 붙일 수 있음. 
4. render()
5. componentDidUpdate() : 렌더 이후엔 로딩중 메세지는 여기서 숨기면 됨

#### 예시

``` jsx
class App extends Component {
    componentWillMount() {}
    render() {}
    componentDidMount() {}
}
```



## 6. state

* component 안의 state가 변결될 때마다, render가 발생한다.

* 즉, state를 변경하면, 새로운 state와 함께 render가 다시 작동한다.
* `props`가 변동되지 않는 데이터를 다룰 때 사용한다면, `state`는 유동적인 데이터를 다룰 때 사용한다.
* state를 변경할 땐 setState() 메소드를 활용한다.

``` jsx
class App extends Component {
	...
  componentDidMount() {
    
    setTimeout( () => {
      this.setState( {
        movies: [
          ...this.state.movies, // 이전꺼는 그대로 둠
          {
            title: "Trainspotting",
            poster: "https://t1.daumcdn.net/cfile/tistory/204B7D4A4E99A1FA2C"
          }
        ]
      })
    }, 1000)
  }
}
```



## 7. Smart Component, Dumb Component

state가 있고, render()를 해줘야 하는 component는 Smart Component.

props를 받아서, html 요소를 리턴만 해주는 함수형태의 component를 Dumb Component라고 한다.

* Dumb Component 예시

```jsx
Movie.propTypes = {
    title: PropTypes.string.isRequired,
    poster: PropTypes.string.isRequired
}

function Movie({title, poster}) {
    return (
        <div>
            <MoviePoster poster={poster}/>
            <h1>{title}</h1>
        </div>
    )
}

MoviePoster.propTypes = {
    poster: PropTypes.string.isRequired
}

function MoviePoster({poster}) {
    return (
        <img src={poster} alt="movie Poster" />
    )
}
```

업데이트가 필요없고 간단한 출력만 필요할 땐, 이렇게 사용할 수 있다.

## 8. fetch

AJAX를 통해 비동기적으로 URL에 요청하고 응답받을 수 있다. 여기서 비동기적이란 브라우저의 새로고침, 혹은 페이지 전환 없이 수행 가능한 것을 의미한다.

```jsx
componentDidMount() {
    fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
}
```

fetch가 반환하는 것은 Promises 이다.



## 9. Promises

보통 코드는 라인넘버 순서대로 차례로 진행되기 때문에 동기적이라고 할 수 있다. 가령 1번줄 코드가 수행되는 중이라면, 2번줄 코드는 1번줄이 다 끝날 때까지 기다려야만 한다.

반대로 1번줄이 종료와는 무관하게 2번줄의 작업이 수행된다면, 이는 비동기적이라고 할 수 있다.

promise는 비동기적으로 작동한다.

```jsx
componentDidMount() {
    fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
    .then(response =>response.json()) // json형태로 바꿈
    .then(json => console.log(json))
    .catch(err => console.log(err))
}
```

위의 코드에서,

fetch가 성공적으로 이뤄지면 .then을 수행한다. .then이 성공하면 그다음 .then을 수행한다.

.catch는 도중 에러가 발생한경우 에러를 출력한다.  (예외처리 같네??)



### .then이 너무 많아질 경우 코드를 읽기 힘들어지는 CALL BACK HELL 이 발생할 수 있다. 이를 해결하기 위한 방법으로 Async, Await 가 있다.

async 를 선언하면 await를 쓸 수 있다. await는 해당 함수가 완료(성공하던 실패하던)가 될 때까지 기다린다. componentDidMount() 에는 여러 함수의 호출이 있을 수 있기 때문에 가독성을 위해 코드들을 분할하여 메서드화 한 후, 호출하는 형태로 리펙토링 한다.

``` jsx
componentDidMount() {
    this._getMovies()
}

_getMovies = async () => {
    const movies = await this._callApi()
    this.setState({
        movies
    })
}

_callApi = () => {
    return fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
    .then(response =>response.json())
    .then(json => json.data.movies)
    .catch(err => console.log(err))
}
```

