# 함수 심화 학습 1

## 재귀와 스택

- 큰 목표 작업 하나를 동일하면서 간단한 작업 여러 개로 나눌 수 있을 때 유용한 프로그래밍 패턴
- 자기 자신을 호출 할때 재귀라고 부름
- 가장 처음 하는 호출을 포함한 중첩 호출의 최대 개수는 재귀깊이 (recursion depth)이라고 함
- 자바스크립트 엔진은 최대 재귀 깊이를 제한함
  - 만개
  - 십만까지는 다루지 못함
  - 엔진 내부에서 `tail calls optimization` 이라는 최적화로 제한을 완화하려고함

### 실행 컨텍스트와 스택

- 실행 중인 함수의 실행 절차에 대한 정보는 해당 함수의 실행 컨텍스트 (execution context) 에 저장
  - 실행 컨텍스트 : 함수 실행에 대한 세부 정보를 담고 있는 내부 데이터 구조
  - 실행 컨텍스트는 함수 실행에 대한 세부 정보를 담고 있는 내부 데이터 구조
- 함수 내부 중첩 호출
  - 현재 함수의 실행이 일시 중지
  - 중지된 함수와 연관된 실행 컨텍스트는 실행 컨텍스트 스택이라는 특별한 자료구조에 저장
  - 중첩 호출 실행
  - 중첩 호출 실행이 끝난 이후 실행 컨텍스트 스택에서 일시 중단한 함수의 실행 컨텍스트를 꺼내오고, 중단한 함수의 실행을 다시 이어감
- 재귀를 이용해 작성한 코드는 반복문을 사용한 코드로 다시 작성할 수 있음. 반복문을 사용하면 대개 함수 호출 비용(메모리 사용)이 절약
- 재귀를 사용하면 코드가 짧아지고 코드 이해도가 높아지고 유지보수에도 이점이 있음
- 재귀적 순회를 구현시 좋음

## 나머지 매개변수와 전개 문법

### 나머지 매개변수 …

- 함수 정의 방법과 상관없이 함수에 넘겨주는 인수의 개수에 제약이 없음

```javascript
function sumAll(...args) {
  // args는 배열의 이름입니다.
  let sum = 0;

  for (let arg of args) sum += arg;

  return sum;
}

alert(sumAll(1)); // 1
alert(sumAll(1, 2)); // 3
alert(sumAll(1, 2, 3)); // 6
```

- 남아 있는 인수를 모으는 역할을 하므로 나머지 매개변수두의 인수가 있으면 에러가 발생함
  `function f(arg1, ...rest, arg2)()`

### `arguments변수`

- `arguments`특별한 유사 배열 객체를 이용하면 인덱스를 사용해 모든 인수에 접근 가능

```Javascript
function showName() {
  alert( arguments.length );
  alert( arguments[0] );
  alert( arguments[1] );

  // arguments는 이터러블 객체이기 때문에
  // for(let arg of arguments) alert(arg); 를 사용해 인수를 나열할 수 있습니다.
}

// 2, Julius, Caesar가 출력됨
showName("Julius", "Caesar");

// 1, Bora, undefined가 출력됨(두 번째 인수는 없음)
showName("Bora");
```

### spread문법

```javascript
let arr = [3, 5, 1];

alert(Math.max(...arr));
```

- 함수를 호출할 때 `…arr`를 사용하면, 이터러블 객체 arr이 인수 목록으로 확장됨

## 변수의 유효범위와 클로저

- 자바스크립트는 함수 지향 언어
  - 함수를 동적으로 생성
  - 생성한 함수를 다른 함수에 인수로 넘김
  - 생성된 곳이 아닌 곳에서 함수를 호출 할 수 있음

### 코드 블록

- `{…}` 안에서 선언한 변수는 블록 안에서만 사용할 수 있음
- `if`, `for`, `while`등에서도 마찬가지로 `{…}` 안에서 선언한 변수는 오직 블록

### 중첩 함수

- 함수 내부에서 선언한 함수는 `중첩(nested)` 함수라고 부름

```javascript
function sayHiBye(firstName, lastName) {
  // 헬퍼(helper) 중첩 함수
  function getFullName() {
    return firstName + " " + lastName;
  }

  alert("Hello, " + getFullName());
  alert("Bye, " + getFullName());
}
```

- 중첩 함수는 새로운 객체의 프로퍼티 형태나 중첩 함수 그 자체로 반환될 수 있음

### 렉시컬 환경

- 레시컬 환경 (lexical environment)
  - 실행 중인 함수, 코드 블록, 스크립트전체는 내부 숨김 연관 객체를 갖음
  - 두분으로 구성
    - 환경 레코드 : 모든 지역 변수를 프로퍼티로 저장하고 있는 객체. ( this )
    - 왼부 렉시컬 환경에 대한 참조 : 외부 코드와 연관됨
- 변수는 특수 내부객체인 환경 레코드의 프로퍼티
  - 변수를 가져오거나 변경 === 환경 레코드의 프로퍼티를 가져오거나 변경
- 스크립트 전체와 관련된 렉시컬 환경은 전역 렉시컬 환경 (global Lexical Environment)
- 코드가 실행되고 실행 흐름이 이어져 나가면 렉시컬 환경은 변화

## 오래된 var

- var는 블록 스코프가 없음
- var로 선언한 변수의 스코프는 함수 스코프이거나 전역 스코프임

```javascript
if (true) {
  var test = true; // 'let' 대신 'var'를 사용했습니다.
}

alert(test); // true(if 문이 끝났어도 변수에 여전히 접근할 수 있음)
```

- let 에서는 같은 이름의 변수를 선언시에 에러가 뜨지만, var는 뜨지 않는다.

```javascript
var user = "Pete";

var user = "John"; // this "var" does nothing (already declared)
// ...it doesn't trigger an error

alert(user); // John
```

- 선언하기 전에 사용할 수 있음 var
  - 호이스팅 : 변수가 끌어올려지는 현상
  - 선언은 호이스팅이 되지만 할당은 호이스팅되지 않음

```javascript
function sayHi() {
  var phrase; // 선언은 함수 시작 시 처리됩니다.

  alert(phrase); // undefined

  phrase = "Hello"; // 할당은 실행 흐름이 해당 코드에 도달했을 때 처리됩니다.
}

sayHi();
```

- 즉시 실행 함수 표현식 (IIFE)

```javascript
(function () {
  let message = "Hello";

  alert(message); // Hello
})();
```

    - 함수 표현식이 만들어지고 바로 호출하면서 해당 함수가 바로 실행

```javascript
// IIFE를 만드는 방법

(function () {
  alert("함수를 괄호로 둘러싸기");
})();

(function () {
  alert("전체를 괄호로 둘러싸기");
})();

!(function () {
  alert("표현식 앞에 비트 NOT 연산자 붙이기");
})();

+(function () {
  alert("표현식 앞에 단항 덧셈 연산자 붙이기");
})();
```
