## 1. function Component => class Component

-   function Component
    -   function이 return하는 내용을 실행한다.

```js
function App() {
    return (
        <div>
            {foodILike.map(dish => (
                <Food
                    key={dish.id}
                    name={dish.name}
                    image={dish.image}
                    rating={dish.rating}
                />
            ))}
        </div>
    );
}
```

-   class Component는 `React.Component`을 상속받는다.

    -   `render()` 메소드가 return하는 내용을 실행한다.

    ```js
    class App extends React.Component {
        render() {
            return <h1>나는 클래스 컴포넌트</h1>;
        }
    }
    ```

### function Component와 class Component의 차이?

-   class Component에서는 state를 사용할 수 있다.
-   function Component에서는 state를 사용할 수 없어서 `useState`같은 Hook을 이용한다. class Component에서는 Hook을 사용하지 못한다.

## 2. State

state는 Object이고, Component의 data를 넣을 공간을 가지고있다.

-   state가 가지고 있는 data는 변한다.
-   state 내부의 data를 직접 변경할 수 없다.

    ```js
    // 동작하지 않는 코드
    state = {
        count: 0,
    };

    add = () => {
        this.state.count = 1;
    };
    minus = () => {
        this.state.count = -1;
    };

    render() {
        return (
            <div>
                <h1>지금 숫자는 {this.state.count}</h1>
                <button onClick={this.add}>더하기</button>
                <button onClick={this.minus}>빼기</button>
            </div>
        );
    }
    ```

    -   위 코드는 state를 변경하고`render`를 재호출하지 않으므로 화면에 변경사항이 반영되지 않는다.
    -   `setState`를 호출하여 state를 변경할 수 있다.

        ```js
        state = {
            count: 0,
        };

        add = () => {
            this.setState({ count: 1 });
        };
        minus = () => {
            this.setState({ count: -1 });
        };
        ```

        `setState`에 새로운 state를 넘겨주면 state가 재설정되고, `render`를 호출한다.

-   현재 상태를 반영하여 state를 변경하기  
    `setState`에 현재 상태를 인자로 가지는 콜백함수를 전달한다.

```js
class App extends React.Component {
    state = {
        count: 0,
    };

    add = () => {
        this.setState(cur => ({ count: cur.count + 1 }));
    };
    minus = () => {
        this.setState(cur => ({ count: cur.count - 1 }));
    };

    render() {
        return (
            <div>
                <h1>지금 숫자는 {this.state.count}</h1>
                <button onClick={this.add}>더하기</button>
                <button onClick={this.minus}>빼기</button>
            </div>
        );
    }
}
```

## 3. Component Life Cycle

### Life Cycle Method

: react가 component를 생성하고, 없애는 과정

-   컴포넌트를 render 할 때, `render` 메소드만 실행되는 것이 아니라 다른 함수도 호출된다.

    -   ## Mounting: 컴포넌트 생성

        ```js
        class App extends React.Component {
            constructor(props) {
                super(props);
                console.log("constructor");
            }
            componentDidMount() {
                console.log("component rendered");
            }
            render() {
                console.log("render");
                return (
                    <div>
                        <h1>지금 숫자는 {this.state.count}</h1>
                        <button onClick={this.add}>더하기</button>
                        <button onClick={this.minus}>빼기</button>
                    </div>
                );
            }
        }

        //constructor
        //render
        //component rendered
        ```

        -   1. `constructor()`: class 내부의 생성자가 render 전에 실행된다.
        -   2. `static getDerivedStateFromProps()`
        -   3. `render()`
        -   4. `componentDidMount()`: component가 render된 후 실행된다.

    -   ## Updating: 컴포넌트 업데이트

        ```js
        class App extends React.Component {
            componentDidUpdate() {
                console.log("i'm updated!!");
            }
            state = {
                count: 0,
            };

            add = () => {
                this.setState(cur => ({ count: cur.count + 1 }));
            };
            minus = () => {
                this.setState(cur => ({ count: cur.count - 1 }));
            };

            render() {
                console.log("render");
                return (
                    <div>
                        <h1>지금 숫자는 {this.state.count}</h1>
                        <button onClick={this.add}>더하기</button>
                        <button onClick={this.minus}>빼기</button>
                    </div>
                );
            }
        }
        //버튼을 클릭할 때 마다 console에 다음과 같은 내용이 출력된다.
        //render
        //i'm updated!!
        ```

        `setState` 호출 시 다음과 같은 작업이 발생한다.

        -   1. `static getDerivedStateFromProps()`
        -   2. `shouldComponentUpdate()`
        -   3. `render()`
        -   4. `getSnapshotBeforeUpdate()`
        -   5. `componentDidUpdate()`

    -   ## Unmounting: 컴포넌트 삭제
        -   1. `componentWillUnmount()`: 현재 페이지를 벗어나서 컴포넌트를 더이상 사용하지 않게 되었을때 호출된다.

## 실습코드 응용

5초의 로딩이 끝나면 We are Ready를 띄우는 컴포넌트

```js
class App extends React.Component {
    state = {
        isLoading: true,
        seconds: 0,
    };

    componentDidMount() {
        setInterval(() => {
            if (this.state.seconds < 5)
                this.setState(cur => ({
                    isLoading: true,
                    seconds: cur.seconds + 1,
                }));
            else
                this.setState(cur => ({
                    isLoading: false,
                    seconds: 6,
                }));
        }, 1000);
    }

    render() {
        const { isLoading, seconds } = this.state;
        return <div>{isLoading ? "Loading..." + seconds : "We are Ready"}</div>;
    }
}
```
