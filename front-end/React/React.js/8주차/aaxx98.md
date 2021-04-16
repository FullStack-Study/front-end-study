# 1. 깃허브 페이지로 배포

## gh-pages

웹 사이트를 github의 github page 도메인에 나타나게 해줌

```
npm install gh-pages
```

### package.json

```json
{
    "scripts": {
        "start": "react-scripts start",
        "build": "react-scripts build",
        "deploy": "gh-pages -d build",
        "predeploy": "npm run build"
    },

    ...

    "homepage": "https://aaxx98.github.io/movie_app_2019/"
}
```

작성 후 `npm run deploy` 실행

-   deploy -> predeploy-> build

# 2. 라우팅

## react-router-dom

네비게이션을 만들어주는 패키지

```
npm install react-router-dom
```

```js
import React from "react";
import { HashRouter, Route } from "react-router-dom";
import About from "./routes/About";
import Home from "./routes/Home";

function App() {
    return (
        <HashRouter>
            <Route path="/about" component={About} />
        </HashRouter>
    );
}

export default App;
```

-   http://localhost:3000/movie_app_2019#/about 에 About.js를 렌더한다.

```js
<HashRouter>
    <Route path="/" component={Home} />
    <Route path="/about" component={About} />
</HashRouter>
```

다음과 같이 작성하면 Home.js와 About.js의 내용이 동시에 렌더링된다.

```js
<HashRouter>
    <Route path="/" exact={true} component={Home} />
    <Route path="/about" component={About} />
</HashRouter>
```

`exact={true}`를 추가하면 path가 `/`일때만 Home.js를 렌더한다.

## 네비게이션 만들기

```js
import React from "react";

function Navigation() {
    return (
        <div>
            <a href="/">Home</a>
            <a href="/about">About</a>
        </div>
    );
}

export default Navigation;
```

-   `<a href="/">Home</a>` 와 같은 HTML 태그로 링크를 생성하면, page를 새로고침한다.
-   리액트 페이지가 전부 리렌더링 되므로 적절하지 않다.
-   react-router-dom의 **Link**를 사용하면 리렌더링 되지않는다.

    -   Link는 라우터 태그 내부에 있어야한다.
    -   `to`에는 이동할 path를 넘겨준다.

    ```js
    import React from "react";
    import { Link } from "react-router-dom";

    function Navigation() {
        return (
            <div>
                <Link to="/">Home</Link>
                <Link to="/about">About</Link>
            </div>
        );
    }

    export default Navigation;
    ```

    -   Link를 이용하여 링크로 이동하면서 props를 넘겨줄 수 있다.

        -   pathname에 작성한 path로 이동하면서
        -   state 내용을 넘겨준다.

    ```js
    function Movie({ year, title, summary, poster, genres }) {
    return (
        <Link
            to={{
                pathname: "/movie-detail",
                state: {
                    year,
                    title,
                    summary,
                    poster,
                    genres,
                },
            }}
        >Link</Link>

        ...
    )}
    ```

    ![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a2b643d6-4104-4b25-a8dc-10ce70b78b0c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T113702Z&X-Amz-Expires=86400&X-Amz-Signature=f66bce90a823f4ffb720d057ce14c303ba67c394ddf8ba258e445f64e46db76e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)
