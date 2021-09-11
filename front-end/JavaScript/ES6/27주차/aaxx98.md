# 함수 심화 학습

## 1. 재귀와 스택

### 재귀

-   자기 자신을 호출하는 것
-   재귀 깊이(recursion depth)
    -   자바스크립트 엔진은 재귀 깊이 1만 까지 허용
        -   엔진 내부에서 `tail calls optimization` 최적화 수행
    -   대부분 10만 까지는 불가능

### 실행 컨텍스트와 스택

-   실행 컨텍스트(execution context)
    -   함수 실행에 대한 세부 정보를 담고 있는 내부 데이터 구조
    -   함수 호출 1회당 1개의 실행 컨텍스트가 생성된다.
    -   함수 내부에 중첩 호출이 있을 때
        -   현재 함수의 실행이 일시 중지 됨
        -   중지된 함수와 연관된 실행 컨텍스트는 실행 컨텍스트 스택에 저장됨
        -   중첩호출 실행
        -   중첩호출 실행이 끝난 후, 실행 컨텍스트 스택에서 일시 중단한 함수의 실행 컨텍스트를 꺼내오고, 중단한 함수의 실행을 다시 이어감

## 2. 나머지 매개변수와 전개 문법

### 나머지 매개변수 `...`

-   함수 정의 방법과 상관 없이 함수에 넘겨주는 인수의 개수에는 제약이 없다.

    ```js
    function sum(a, b) {
        return a + b;
    }

    // 전달은 가능하나, 세번째 인수부터는 무시된다.
    alert(sum(1, 2, 3, 4, 5));
    ```

-   나머지 매개변수 `...`을 사용하면 여분의 인수를 배열에 담아 전달한다.
    -   나머지 매개변수는 마지막 인수에만 사용 가능

```js
function sumAll(...args) {
    let sum = 0;

    for (let arg of args) sum += arg;

    return sum;
}

alert(sumAll(1)); // 1, args = [1]
alert(sumAll(1, 2)); // 3, args = [1,2]
alert(sumAll(1, 2, 3)); // 6, args = [1,2,3]
```

### `arguments` 변수

-   유사배열 객체 `arguments`

    -   인덱스를 사용해 모든 인수에 접근 가능

        ```js
        function showName() {
            alert(arguments.length);
            alert(arguments[0]);
            alert(arguments[1]);
        }

        // 2, Julius, Caesar
        showName("Julius", "Caesar");

        // 1, Bora, undefined
        showName("Bora");
        ```

    -   이터러블 객체이고 배열은 아니다.
        -   `for(let arg of arguments) alert(arg);` 로 인수 나열 가능
        -   map은 사용할 수 없음
    -   화살표 함수에서 `arguments`는 화살표 함수 외부의 일반 함수의 `arguments`를 가져온다.

        ```js
        function f() {
            let showArg = () => alert(arguments[0]);
            showArg();
        }

        f(1); // 1
        ```

### spread 문법

-   `...`을 사용하면 배열을 인수 목록으로 확장한다.

```js
let arr = [3, 5, 1];

alert(Math.max(arr)); // NaN
alert(Math.max(...arr)); // 5
```

## 3. 변수의 유효범위와 클로저

### 코드 블록

-   코드 블록 `{...}` 안에서 선언한 변수는 블록 안에서만 사용 가능
    -   `if`, `for`, `while`도 코드블록을 가짐
-   특정 작업을 수행하는 코드를 한데 묶어두는 용도로 사용
-   같은 코드 블록 내에서 같은 변수를 두번 이상 `let`으로 선언할 수 없음.

### 중첩 함수 (nested function)

-   함수 내부에서 선언한 함수

```js
function makeCounter() {
    let count = 0;

    return function () {
        return count++;
    };
}

let counter = makeCounter(); // [count를 반환하는 함수] 반환

// makeCounter 내의 count contex가 유지된다.
alert(counter()); // 0
alert(counter()); // 1
alert(counter()); // 2
```
