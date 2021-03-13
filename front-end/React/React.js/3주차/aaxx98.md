## mashup-todolist

![구조](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef2cf6cc-9bed-43cd-ace1-c915e09f22b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210313T032407Z&X-Amz-Expires=86400&X-Amz-Signature=856f7d360466a9e7d9f69a1cfd4e92d4f0f17172330846cc742caba5688c95bd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

-   **TodoTemplate**

    투두리스트의 레이아웃을 설정하는 컴포넌트

    페이지의 중앙에 그림자가 적용된 흰색 박스를 보여줍니다.

-   **TodoHead**

    오늘의 날짜와 요일을 보여주고, 앞으로 해야 할 일이 몇개 남았는지 보여줍니다.

-   **TodoList**

    할 일에 대한 정보가 들어있는 todos 배열을 내장함수 `map` 을 사용하여 여러개의 TodoItem 컴포넌트를 렌더링해줍니다.

-   **TodoItem**

    각 할 일에 대한 정보를 렌더링해주는 컴포넌트입니다.

    좌측에 있는 원을 누르면 할 일의 완료 여부를 toggle 할 수 있습니다.

    할 일이 완료됐을 땐 좌측에 체크가 나타나고 텍스트의 색상이 연해집니다.

    그리고, 마우스를 올리면 휴지통 아이콘이 나타나고 이를 누르면 항목이 삭제됩니다.

-   **TodoCreate**

    새로운 할 일을 등록할 수 있게 해주는 컴포넌트

    TodoTemplate 의 하단부에 초록색 원 버튼을 렌더링해주고, 이를 클릭하면 할 일을 입력 할 수 있는 폼이 나타납니다.

    버튼을 다시 누르면 폼이 사라집니다.

    # styled-components

    [styled-components 자세한 내용](https://react.vlpt.us/styling/03-styled-components.html)

    리액트 프로젝트에 전체 css를 설정하는 모듈

    ```bash
    yarn add styled-components
    또는
    npm install --save styled-components
    ```

    App.js

    ```jsx
    import React from "react";
    **import { createGlobalStyle } from "styled-components";**

    **const GlobalStyle = createGlobalStyle`
      body{
        background: #e9ecef;
      }
    `;**
    function App() {
        return (
            <>
                **<GlobalStyle />**
                <div>안녕하세요</div>
            </>
        );
    }

    export default App;
    ```
