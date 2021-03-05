# 리액트
## React란?
사용자 인터페이스를 구축하기 위한 선언적, 효율적, 유연한 JavaScript 라이브러리

**컴포넌트**라고 불리는 작고 고립된 코드의 파편을 이용해서 복잡한 UI를 구성하도록 돕는다.

리액트는 앱처럼 동작하는 웹 = **Web-app**을 만들 때 용이하다.

: 새로고침 없이 화면전환(ex. 인스타그램과 같은 sns 페이지)
- 장점
    - 모바일 앱으로 전환하기 쉽다.
    - 앱처럼 뛰어난 UX


## 간단한 사용법

```js
class Subject extends Component{ //Subject라는 이름의 사용자 정의 태그 선언
    function render(){
        return(
            <header>
                <h1>WEB</h1>
                World wide web
            </header>
        );
    }
}

class App extends Component{
    render(){ 
        return(
                                    //    <header>
            <Subject></Subject>     //        <h1>WEB</h1>
                                    //        World wide web
                                    //    </header>
        );
    }
}
```
다음 코드 처럼, 사용자 정의 태그를 선언해두고 활용할 수 있다.

- React.Component 클래스를 상속받아서 `render`에 표시할 내용을 정의한다.
- `Subject`는 **React.Component 클래스** 또는 **React.Component 타입**이다.
- `render` 함수는 화면에서 보고자 하는 내용을 반환한다. 뷰 계층 구조를 반환한다.
- `render` 함수는 렌더링할 내용을 경량화한 React 엘리먼트를 반환하는데, 리액트에서는 **JSX** 라는 특수한 문법이 사용된다.   
    - JSX는 JavaScript를 확장한 문법으로 React element를 생성한다.
    - `<header>` 구문은 빌드하는 시점에서 `React.createElement('header' ...)`로 변환된다.
        ```js
        //<Subject></Subject>는 다음과 같이 변환됨
        return React.createElement('header', null,
            React.createElement('h1', null, "WEB")
            , "World wide web"
        );
        ```
    
## 프로퍼티(props)
```js
//property => props 프로퍼티
class Subject extends Component{ //Subject라는 이름의 사용자 정의 태그 선언
    function render(){
        return(
            <header>
                <h1>{this.props.title}</h1>
                {this.props.sub}
            </header>
        );
    }
}

class App extends Component{
    render(){ 
        return(
                                                                    //    <header>
            <Subject title="WEB" sub="World wide web"></Subject>    //        <h1>WEB</h1>
                                                                    //        World wide web
                                                                    //    </header>
        );
    }
}
```
다음과 같이 `props`를 이용하여 태그로부터 매개변수를 받아와 렌더링하는 것도 가능하다.
- 구조는 같지만 내용은 다른 UI를 구성할 수 있다.

## state

```js
...
class TOC extends Component{ //Subject라는 이름의 사용자 정의 태그 선언
    function render(){
        return(
            <nav>
                <ol>
                    <li><a href="1.html">HTML</a></li>
                    <li><a href="2.html">CSS</a></li>
                    <li><a href="3.html">JavaScript</a></li>
                </ol>
            </nav>
        );
    }
}

class App extends Component{
    render(){ 
        return(    
            <TOC data={this.state.contents}></TOC>
        );
    }
}
```
다음 코드는 아래와 같이 `<li>`를 list로 만들어서 작성할 수 있다.
```js
...
class TOC extends Component{ //Subject라는 이름의 사용자 정의 태그 선언
    function render(){
        var list = [
            <li><a href="1.html">HTML</a></li>,
            <li><a href="2.html">CSS</a></li>,
            <li><a href="3.html">JavaScript</a></li>,
        ];
        return(
            <nav>
                <ol>
                    {list}
                </ol>
            </nav>
        );
    }
}

class App extends Component{
    render(){ 
        return(    
            <TOC data={this.state.contents}></TOC>
        );
    }
}
```
list 내용을 for문과 state를 통해 갱신할 수 있다.
```js
...
class TOC extends Component{ //Subject라는 이름의 사용자 정의 태그 선언
    function render(){
        var list = [];
        var i = 0;
        while(i<this.props.data.length){
            var data = this.props.data[i];
            list.push(<li key={data.id}><a href={data.id + '.html'}>{data.title}</a></li>);
            i++;
        }
        return(
            <nav>
                <ol>
                    {list}
                </ol>
            </nav>
        );
    }
}

class App extends Component{
    render(){ 
        state = {
            contents:[
                {id:1, title:'HTML', desc:'HTML 어쩌구저쩌구'},
                {id:2, title:'CSS', desc:'CSS 어쩌구저쩌구'},
                {id:3, title:'JavaScript', desc:'JavaScript 어쩌구저쩌구'},
            ]
        }
        return(    
            <TOC data={this.state.contents}></TOC>
        );
    }
}
```
보통 React.Component 타입의 생성자(`constructor()`)에 this.state를 설정하는 것으로 state를 추가해주는 방식을 사용한다.
- `this.state`는 정의된 React.Component 클래스 내부에서만 조작할 수 있도록 하는 것이 좋기 때문이다.
    ```js
    class Square extends React.Component { 
        constructor(props){ //Square의 생성자
            super(props); //생성자를 정의할 때 반드시 super(props)를 호출해야 함 - 부모속성 정의
            this.state = { //생성자 내부에서 state 속성을 추가한다.
                value: null,
            };
        }

        render() {
            return (
                ...
            );
        }
    }
    ```

## 부모 컴포넌트가 제어하는 state
- 부모 컴포넌트(`Board`)는 자식 컴포넌트(`Square`)를 호출(?)한다.
- `Square`의 상태는 `Board`에서 관리하는 것이 적절하다.
    - 여러 자식을 가지는 컴포넌트에서 자식 컴포넌트 간 통신을 하려면 부모 컴포넌트에 state을 정의한다.
    - 부모 컴포넌트는 props를 이용하여 자식 컴포넌트에 state을 전달할 수 있으므로 자식 컴포넌트간의 동기화나 부모-자식 컴포넌트 간의 동기화에 유용하다.
    
    `Board`의 `state.squares`에서 관리하는 코드는 다음과 같다.
```js
class Square extends React.Component { //버튼<button> 렌더링
  render() {
      return ( //버튼을 클릭하면 onClick 속성에 연결된 함수가 실행됨
        <button 
          className="square" 
          onClick={() => this.props.onClick()} 
        >
          {this.props.value} 
        </button>
      );
  }
}
  
class Board extends React.Component { //사각형 9개를 렌더링
  constructor(props){ 
    super(props);
    this.state = { //Squre과 공유할 수 있는 state
      squares: Array(9).fill(null), //9개의 null로 채운 배열
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice(); //this.state의 복사본
    squares[i] = 'X';
    this.setState({squares: squares}); //복사본을 this.state에 덮어 씌우는 방식으로 갱신
  }

  renderSquare(i) { //Square 태그를 사용하는 함수
      return (
        <Square 
          value={this.state.squares[i]}
          onClick={() => this.handleClick(i)}
        />
      );
  }
  
  render() {
      const status = 'Next player: X';
  
      return (
        <div>
          <div className="status">{status}</div>
          <div className="board-row">
            {this.renderSquare(0)}
            {this.renderSquare(1)}
            {this.renderSquare(2)}
          </div>
          <div className="board-row">
            {this.renderSquare(3)}
            {this.renderSquare(4)}
            {this.renderSquare(5)}
          </div>
          <div className="board-row">
            {this.renderSquare(6)}
            {this.renderSquare(7)}
            {this.renderSquare(8)}
          </div>
        </div>
      );
  }
}
  
```
동작 흐름은
1. 화면에서 사각형 버튼 클릭 `<button className="square"  onClick={() => this.props.onClick()} > {this.props.value} </button>`
2. `this.props.onClick()`이 실행되어 부모 컴포넌트 `Board`로 부터 매개변수 `onClick`으로 전달받은 함수가 실행된다.
```js
<Square 
    value={this.state.squares[i]}
    onClick={() => this.handleClick(i)} //이 부분
/>
```

3. `Board`의 `handleClick(i)`가 실행된다.
    - `handleClick(i)`는 state.squares를 갱신하고, state가 갱신되면 화면이 render된다.


## 함수 컴포넌트
- 간단한 구조의 컴포넌트는 함수로 작성할 수 있다. 함수 컴포넌트는 state 없이 `render` 함수만을 가진다.
```js
class Square extends React.Component { 
  render() {
      return ( 
        <button 
          className="square" 
          onClick={() => this.props.onClick()} 
        >
          {this.props.value} 
        </button>
      );
  }
}
```
함수 컴포넌트로 바꾸기
```js
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```
> 주의
> `onClick={props.onClick}`에서 함수가 양쪽 모두 괄호가 사라진 형태로 바뀌었음