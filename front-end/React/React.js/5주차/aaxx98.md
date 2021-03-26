# React

## 구조

-   리액트 프로젝트에서 첫 화면(localhost:3000)은 `public/index.html`이다.
-   이 html 파일을 직접 수정하지 않고, src 폴더의 코드를 JSX라는 특별한 문법을 이용하여 읽어서 HTML 뷰를 생성함
-   `index.html`내부 태그에 컴포넌트를 삽입하여 render한다.

-   컴포넌트는 HTML 코드를 반환하는 함수이다.  
    ex) `src/Potato.js`

        ```js
        import React from "react";

        function Potato() {
            return <h3>I love potato</h3>;
        }

        export default Potato;
        ```

### 1. index.html

![index.html](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/419baa3c-d0cf-4e1c-8d50-1cf5ec62d4e0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210326%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210326T163403Z&X-Amz-Expires=86400&X-Amz-Signature=ab4b3828c48efce322fb4e712ca610c6aaab62b1a052fbd0e4c1c5b35aa9a5fd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### 2. `src/index.js`

-   id="root"인 태그 사이에 컴포넌트 `App`을 삽입한다. (App은 `<div>hello~</div>`를 return함)

    ```js
    ReactDOM.render(<App />, document.getElementById("root"));
    ```

### 3. 화면은 다음과 같다.

![화면](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2f52b5c6-eae6-4d83-86ce-67cb82542054/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210326%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210326T163541Z&X-Amz-Expires=86400&X-Amz-Signature=e5708b5af17d48e780e8a295c84c59d330eb0d0ef3e5d13e4f4b3f1cb11133fc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

## props

```js
function App() {
    return (
        <div>
            <h1>hello</h1>
            <Food favorite="김치" />
            <Food favorite="삼겹살" />
            <Food favorite="쭈꾸미" />
            <Food favorite="라면" />
        </div>
    );
}

function Food({ favorite }) {
    return <h3>I love {favorite}</h3>;
}

export default App;
```

`<컴포넌트이름 속성=전달할값>`으로 태그를 작성하면 Food에 인자로 전달된다.  
`<컴포넌트이름 속성1=값1 속성2=값2 속성3=값3>`
속성을 여러개 전달할 수도 있다.

```js
{
    속성1 = 값1;
    속성2 = 값2;
    속성3 = 값3;
}
```

다음과 같은 형태의 인자로 전달된다.

## array.map으로 컴포넌트 생성

```js
function App() {
    return (
        <div>
            {foodILike.map(dish => (
                <Food name={dish.name} image={dish.image} />
            ))}
        </div>
    );
}

const foodILike = [
    {
        name: "Kimchi",
        image:
            "http://aeriskitchen.com/wp-content/uploads/2008/09/kimchi_bokkeumbap_02-.jpg",
    },
    {
        name: "Samgyeopsal",
        image:
            "https://3.bp.blogspot.com/-hKwIBxIVcQw/WfsewX3fhJI/AAAAAAAAALk/yHxnxFXcfx4ZKSfHS_RQNKjw3bAC03AnACLcBGAs/s400/DSC07624.jpg",
    },
    {
        name: "Bibimbap",
        image:
            "http://cdn-image.myrecipes.com/sites/default/files/styles/4_3_horizontal_-_1200x900/public/image/recipes/ck/12/03/bibimbop-ck-x.jpg?itok=RoXlp6Xb",
    },
    {
        name: "Doncasu",
        image:
            "https://s3-media3.fl.yelpcdn.com/bphoto/7F9eTTQ_yxaWIRytAu5feA/ls.jpg",
    },
    {
        name: "Kimbap",
        image:
            "http://cdn2.koreanbapsang.com/wp-content/uploads/2012/05/DSC_1238r-e1454170512295.jpg",
    },
];

function Food({ name, image }) {
    return (
        <div>
            <h2>I love {name}</h2>
            <img src={image} />
        </div>
    );
}

export default App;
```

-   다음과 같이 작성하면 console에 warning이 발생함

![warning](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/30df2717-00b7-4697-aa32-959faedfa675/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210326%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210326T172453Z&X-Amz-Expires=86400&X-Amz-Signature=3f3193c12b4db5dca0016e6febbd110ec65db73cd941dadeae7a6a180aac2969&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

key 값을 만들어서 전달해주면 해결된다.

```js
function App() {
    return (
        <div>
            {foodILike.map(dish => (
                <Food key={dish.id} name={dish.name} image={dish.image} />
            ))}
        </div>
    );
}

const foodILike = [
    {
        id: 1,
        name: "Kimchi",
        image:
            "http://aeriskitchen.com/wp-content/uploads/2008/09/kimchi_bokkeumbap_02-.jpg",
    },
    {
        id: 2,
        name: "Samgyeopsal",
        image:
            "https://3.bp.blogspot.com/-hKwIBxIVcQw/WfsewX3fhJI/AAAAAAAAALk/yHxnxFXcfx4ZKSfHS_RQNKjw3bAC03AnACLcBGAs/s400/DSC07624.jpg",
    },
    {
        id: 3,
        name: "Bibimbap",
        image:
            "http://cdn-image.myrecipes.com/sites/default/files/styles/4_3_horizontal_-_1200x900/public/image/recipes/ck/12/03/bibimbop-ck-x.jpg?itok=RoXlp6Xb",
    },
    {
        id: 4,
        name: "Doncasu",
        image:
            "https://s3-media3.fl.yelpcdn.com/bphoto/7F9eTTQ_yxaWIRytAu5feA/ls.jpg",
    },
    {
        id: 5,
        name: "Kimbap",
        image:
            "http://cdn2.koreanbapsang.com/wp-content/uploads/2012/05/DSC_1238r-e1454170512295.jpg",
    },
];

function Food({ name, image }) {
    return (
        <div>
            <h2>I love {name}</h2>
            <img src={image} alt={name} />
        </div>
    );
}

export default App;
```

## prop-types

전달 받은 props를 확인해줌

```
컴포넌트이름.propTypes = {
    propname: ...
}
```

-   `PropTypes.타입`으로 타입을 설정한다.

-   `.isRequired`는 undefined를 허용하지 않는다.

```js
import PropTypes from "prop-types";

Food.propTypes = {
    name: PropTypes.string.isRequired,
    image: PropTypes.string.isRequired,
    rating: PropTypes.number.isRequired,
};
```
