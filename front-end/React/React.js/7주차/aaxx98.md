# data Fetch (데이터 가져오기)

네트워크 요청을 JSON으로 쉽게 활용하기 위해서 Axios를 사용한다.  
`fetch()` 형태로 사용할 수 있는 Fetch API가 있지만 여기서는 Axios를 사용한다.

## Axios

Axios는 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리이다.

```shell
npm i axios
```

## Promise

`Promise` 객체는 비동기 작업의 상태와 결과 값을 나타낸다.

-   상태
    -   대기(pending): 초기 상태
    -   이행(fulfilled): 연산 성공
    -   거부(rejected): 연산 실패(어떤 오류같은 이유 때문에 거부될 수 있다.), `then` 메서드를 실행한다.

## async, await

-   비동기 함수 `async function`으로 함수를 선언한다.
-   `await` 다음에 오는 표현식이 실행완료 될 때 까지 대기한다.

```js
getMovies = async () => {
    const {
        data: {
            data: { movies },
        },
    } = await axios.get(
        "https://yts-proxy.now.sh/list_movies.json?sort_by=rating"
    );
    this.setState({ movies, isLoading: false });
};
```
