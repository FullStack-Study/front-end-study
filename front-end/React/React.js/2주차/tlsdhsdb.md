# React Tutorial

 

 

## Props 를 통해 데이터 전달하기

 

 

 

부모 Board 컴포넌트에서 자식 Square 컴포넌트로 “prop을 전달”하기

 

``` react

class Square extends React.Component {

  render() {

    return <button className="square">{this.props.value}</button>;

  }

}

 

class Board extends React.Component {

  renderSquare(i) {

    return <Square value={i} />;

  }

 

  render() {

    const status = "Next player: X";

 

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

 

class Game extends React.Component {

  render() {

    return (

      <div className="game">

        <div className="game-board">

          <Board />

        </div>

        <div className="game-info">

          <div>{/* status */}</div>

          <ol>{/* TODO */}</ol>

        </div>

      </div>

    );

  }

}

```

 

 

 

`Board` ➡️ `this.renderSquare(1)`➡️ `<Square value={i} />` ➡️`<button className="square">{this.props.value}</button>`

 

Game 클래스에서 Board component 호출 ➡️ Board 컴포넌트에 있는 `renderSquare` 함수 호출 ➡️` renderSqaure` 함수는  `Square` 호출 ➡️ 여기로 전달된 `props`의 `value `값을 가진 버튼을 리턴하면 그것이 보이는 것.

 

 

 

## 사용자와 상호작용하는 컴포넌트 만들기

 

 

 

Square 컴포넌트를 클릭하면 “X”가 체크되도록하기

 

``` react

render() {

    return <button className="square" onClick = {

      () => this.setState({

        value : 'X'

      })

    }>{this.props.value}</button>;

  }

```

 

`button` 클릭시 상태변수를 x로 변경.

 

 

 

## State 끌어 올리기

 

 

 

`Board` 가 각 `Sqaure` 에 `Sqaure` 의 `state` 를 요청하는 것 보단 부모 컴포넌트인 Board 컴포넌트에 상태를 저장하고 자식 컴포넌트에 props로 전달하여 무엇을 표시할지 보여주는 것이 좋다.더불어 여러개의 자식 컴포넌트를 가질때 자식 컴포넌트끼리 통신하게 하려면 부모 컴포넌트에 공유 `state`를 정의해야한다.

 

```react

class Board extends React.Component {

  constructor(props) {

    super(props);

    this.state = {

      squares: Array(9).fill(null),

    };

  }

 

  renderSquare(i) {

    return <Square value={i} />;

  }

```



해당 값으로 null을 가진 길이가 9인 배열을 상태변수의 초깃값으로 설정한다.



``` react

class Square extends React.Component {

  constructor(props) {

    super(props);

    this.state = {

      value: null

    };

  }

  render() {

    return (

      <button className="square" onClick={() => this.props.onClick()}>

        {this.props.value}

      </button>

    );

  }

}

 

class Board extends React.Component {

  constructor(props) {

    super(props);

    this.state = {

      squares: Array(9).fill(null)

    };

  }

  handleClick(i) {

    const squares = this.state.squares.slice();

    squares[i] = "X";

    this.setState({

      squares: squares

    });

  }

  renderSquare(i) {

    return (

      <Square

        value={this.state.squares[i]}

        onClick={() => this.handleClick(i)}

      />

    );

  }

```

 

##  불변성



```react
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// 이제 player는 변하지 않았지만 newPlayer는 {score: 2, name: 'Jeff'}입니다.

// 만약 객체 spread 구문을 사용한다면 이렇게 쓸 수 있습니다.
// var newPlayer = {...player, score: 2};
```



객체의 불변성을 위해 객체를 복사한뒤 수정하는 방식으로 사용함.



## 함수 컴포넌트?

> state 없이 `render` 함수만을 가집니다. `React.Component`를 확장하는 클래스를 정의하는 대신 `props`를 입력받아서 렌더링할 대상을 반환하는 함수를 작성할 수 있습니다. 함수 컴포넌트는 클래스로 작성하는 것보다 빠르게 작성할 수 있으며 많은 컴포넌트를 함수 컴포넌트로 표현할 수 있습니다.



 ```react
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
 ```



