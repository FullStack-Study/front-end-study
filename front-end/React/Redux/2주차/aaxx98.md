# 리덕스
## Redux란?
- 자바스크립트 어플리케이션을 위한 라이브러리
- 어플리케이션 상태를 저장, 관리
- React-redux를 통해 리액트에 사용

## 필요한 이유
리액트 컴포넌트들이 다음과 같은 구조로 구성되어있다고 하자.

![컴포넌트 예시](https://i.imgur.com/c6A4cHg.png)
- 리액트 프로젝트에서 대부분의 작업은 부모 컴포넌트가 중간자 역할을 하는데, 프로젝트 규모가 커지면 컴포넌트 간 통신에서 여러 컴포넌트를 거쳐야 하는 경우가 발생하고, state 관리도 어려워진다.
- 리덕스를 이용하면 컴포넌트 밖의 리덕스 스토어에서 state를 효율적으로 관리할 수 있게 된다. 

## 기본 개념
![컴포넌트 개념](https://t1.daumcdn.net/cfile/tistory/99CB65345CEFD1690F)
1. component: 각 컴포넌트
2. action: 상태에 변화가 발생하면 액션 객체가 발생함, `type`이라는 value를 반드시 가져야 한다.
- ex. 기존 값 보다 2를 증가시킨 액션
    ```js
    {type: 'INCREMENT', diff: 2}
    ```
3. reducer: 변화를 일으키는 함수, `state`, `action`을 파라미터로 받고 새로운 state 객체를 반환한다.
4. store: state 정보를 저장하는 공간, 리덕스 스토어
5. `subscribe(listener)`: 컴포넌트가 store를 구독한다. 스토어에서 state 변화가 감지되면 `listener` 함수를 호출해준다. 컴포넌트는 새로운 state를 알게 되고, 다시 `render`한다.
6. `dispatch(action)`: 컴포넌트에서 state 변화가 생기면 `dispatch`를 호출한다. 이 때, action 객체를 매개변수로 전달해주어 어떤 type의 변화가 발생했는지 알려준다.