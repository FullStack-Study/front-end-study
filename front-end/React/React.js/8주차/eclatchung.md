#  ReactJS로 영화 웹 서비스 만들기 - 04

## HOOK
### 만들게 된 계기
1. 컴포넌트 사이에서 상태와 관련된 로직을 재사용되기 어려움
2. 복잡한 컴포넌트들은 이해하기 어려움
3. Class는 혼동되기 쉬움

```javascript
import {useState} from 'react';

..함수 컴포넌트안
const [count , setCount] = useState(0);
...
```

`useSate(0);`
- 초기값(초기화)를 받음
- 현재의 state값과 이값을 업데이트 하는 함수를 쌍으로 제공( 배열 구조 분해 문법 (restructuring))

```javascript
var a,b;

[a,b] = [1,2];
console.log(a); //1
console.log(b) //2
```

### 규칙
1. 최상위에서만 HOOK 호출
2. React 함수 컴포넌트 내에서만 사용

### 종류?
- state
- effect

## React build 와 서버 연결
### Node.js Express 기준
- 서버가 두개 사용될때, ⇒ react(localhost:3000) , express.js(localhost:3001)
	- 프록시를 사용해야함
	- 프록시 : 서버와 클라이언트 상의 중계기로서 대리로 통신을 수행함
	- 리액트에서 모듈 ‘ http-proxy-middleware’사용
	- 서버에서 CORS 설정
- build로 서버사용시 ⇒ 빌드시에 react에서 서버 사용을 하지 않음
	- express.js에서 

```javascript
app.use(express.static(path.join(__dirname, ${build파일 위치});
```
TODO 서버 사이드 렌더링에 대해서.. 알아보기…


https://velopert.com/2937
https://jeonghwan-kim.github.io/2018/08/19/express-travis-beanstalk.html

## Reat-Router
```javascript
import {Link} from 'react-router-dom';
...


..
<Link >
..
```

### `Route`컴포넌트
- 라우트 설정시에는 `Route`컴포넌트를 사용하고 `path`값을 설정한다. 
- `exact` : 주어진 경로와 정확히 맞아 떨어져야만 설정한 컴포넌트를 보여줌.
```javscript
import React, { Component } from 'react';
import { Route } from 'react-router-dom';
import { Home, About } from 'pages';


class App extends Component {
    render() {
        return (
            <div>
                <Route exact path="/" component={Home}/>
                <Route path="/about" component={About}/>
            </div>
        );
    }
}

export default App;

```

- 만약에 /에 `exact`를 설정 안할시에는 `/about`에서 `/`도 매칭이 되어서 보여 줌.
- 파라미터
	- `history` : `push`, `replace`를 통해 리다이렉트, 페이지 전환 가능함
	- `location` 현재 경로에 대한 정보를 지니고 있음
	- `match` : 어떤 라우트에 매칭이 되어있는 정보가 있음 

### `Link`컴포넌트
- `<a href=""></a>` 형식으로 사용하면 안되는 이유 ⇒ 새로고침을 하기 때문임.
- 새로고침을 막기 위해서 `Link`컴포넌트 사용 ⇒ 화면 전환
```javascript
<Link to="/"></Link>
```


[react-router :: 1장. 리액트 라우터 사용해보기 | VELOPERT.LOG](https://velopert.com/3417)