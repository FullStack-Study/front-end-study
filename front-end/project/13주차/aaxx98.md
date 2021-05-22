# react-router-dom

react-router-dom을 이용하여 프로젝트 설명 페이지 라우팅

-   App.js

```js
function App() {
    return (
        <HashRouter>
            <Route path="/" exact={true} component={Home} />
            <Route path="/project/:project" component={Detail} />
        </HashRouter>
    );
}
```

-   Project.js
    -   React Router가 location.pathname과 주소창의 URL 경로를 비교하고, path가 일치하면 렌더한다.
    -   location.state로 접근하여 project 정보를 얻어올 수 있다.

```js
function Project({ id, title, tags, date, contents }) {
    return (
        <Link
            to={{
                pathname: `/project/${title}`,
                state: {
                    id,
                    title,
                    tags,
                    date,
                    contents,
                },
            }}
        >
            <div className="project">
                <span className="title">{title}</span>
                <span className="date">{`(${date[0]} ~ ${date[1]})`}</span>
                <div className="skills">
                    {tags.map(e => {
                        return (
                            <span
                                style={{ backgroundColor: coloring() }}
                                className="tag"
                            >
                                {e}
                            </span>
                        );
                    })}
                </div>
                <div className="contents">{contents}</div>
            </div>
        </Link>
    );
}
```
