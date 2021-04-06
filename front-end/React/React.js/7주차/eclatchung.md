#  ReactJS로 영화 웹 서비스 만들기 - 03 ( Data Fetching)

## Data Fetching 
`fetching`은 `Ajax` 방식 중 하나이다.

### 비동식 방식  `Ajax`란?
- `Asynchronous Javascript And XML`
- 전체 페이지를 새로 고치지 않고도 페이지의 일부만을 위한 데이터를 로드하는 기법
- 서버와 자유롭게 통신 (`XHR` : XMLHttpRequest) 가능
- 페이지 깜빡임 없임 `seamless`하게 작동 ⇒ `Javascript`와 `DOM` 이용
리액트에서 `AJAX`구현시 javascript의 내장 객체 `XMLRequest`를 사용하거나, `HTTP Client`을 사용

#### `axios`와 `Fetch API`
- `Fetch API`는 자바스크리브 built-in 라이브러리 
* `Fetch()`는 `body` 프로퍼티를 사용하고, `axios`는 `data` 프로퍼티를 사용함
* `Fetch`의 `url`이 `Fetch()함수의 인자`로 들어가고, `axios`에서는 `url`이 `option객체`로 들어감
* `Fetch`에서 `body`부분은 `stringify()`로 되어짐

### `Axios`
- Node.js를 위한 `Promise API`를 활용하는 HTTP 비동기 통신 라이브러리
- 요청과 응답 데이터의 변형
- HTTP 요청 취소 및 요청과 응답을 JSON 형태로 자동 변경 
#### GET
```javascript
axios.get(url,[,config])
``` 
#### POST
```javascript
axios.post("url주소",{data객체,[,config])
```
#### DELETE
```javascript
axios.delete(url,[,config])
```
#### PUT
```javascript
axios.put(url[,data[,config])
```

출저 : 
- [React | axios란? (feat. Fetch API)](https://velog.io/@shin6403/React-axios%EB%9E%80-feat.-Fetch-API)
- [axios  -  npm](https://www.npmjs.com/package/axios)

## Async Await
- `Promise`를 좀더 쉽게 사용할 수 있게 해줌
- `function` 앞에 `async`를 붙이면 해당 함수는 항상 **프로미스를 반환**해줌
- 프로미스가 아닌 값을 반환하더라도 이행 상태의 프로미스(resolved promise)로 값을 감싸 이행된 프로미스가 반환되도록 함
- `await`키워드를 자바스크립트가 만나면 프로미스가 처리(`settled`)될때까지 기다림.
- 프로미스가 처리될 때까지 함수 실행을 기다림⇒ CPU 리소스 낭비 되지 않음
- 가독성이 Promise보다 나음
- 일반 함수에서는 `await`를 사용할 수가 없음

### `Promise` 3가지 상태
- `pending` : 보류, 초기의 상태이고 현재 내부 작업이 수행중인 상태
- `fulfilled` : 이행, 내부 작업이 성공적으로 수행되었으며 연관된 결과값으 가지고 있는 상태
- `rejected` : 실패, 내부 작업이 실패하였고 그와 연관된 오류값을 가지고 있는 상태.
- `settled` : 정착생태, `pending`이 아닌 상태 : 이행, 실패 상태

![프로미스 3가지 상태](https://media.vlpt.us/images/gcback/post/f3ff82c7-d4f5-4009-9c7f-f40a2b165ce2/assets_mastering-async-await-by-valeri-karpov_-M7wttcClBd7IHemDwBd_-M7wu52KqXyH1h6g_3A0_Cap_2020-05-02_01-38-25-628.png)

## Style Component
- 라이브러리
- 복잡성 제거
- 클래스 대신 props


