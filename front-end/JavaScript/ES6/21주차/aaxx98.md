# 객체

## 1. 객체

### 생성

```js
let user = new Object(); // 객체 생성자
let user = {
    name: "John".
    age: 30
}; // 객체 리터럴 (키:값 프로퍼티)
```

### 리터럴과 프로퍼티

-   프로퍼티 값 삭제
    ```js
    delete user.age;
    ```
-   띄어쓰기가 있는 프로퍼티 이름
    따옴표로 묶는다.
    ```js
    let user = {
        name: "John".
        age: 30,
        "like birds": true
    };
    ```
    -   띄어쓰기가 있는 프로퍼티에 접근
        대괄호 표기법 사용
    ```js
    user["likes birds"];
    ```

### 상수 객체

-   상수 객체의 내용은 수정될 수 있다.

    ```js
    const user = {
        name: "John",
    };

    user.name = "Pete";

    alert(user.name); // Pete
    ```

### `in` 연산자

-   프로퍼티 존재 여부 확인

    -   key는 반드시 따옴표로 감싼 문자열이어야한다.

    ```js
    "key" in object;

    let user = { name: "John", age: 30 };
    console.log("age" in user); // true

    let user = { age: 30 };
    let key = "age";
    console.log(key in user); // true
    ```

### `for...in` 반복문

-   객체 내의 모든 프로퍼티 순회

    ```js
    let user = {
        name: "John",
        age: 30,
        isAdmin: true,
    };

    for (let key in user) {
        alert(key); // name, age, isAdmin
        alert(user[key]); // John, 30, true
    }
    ```

## 2. 참조에 의한 객체 복사

-   객체는 참조에 의해(by reference) 저장되고 복사된다.
-   참조값이 다르면 서로 다른 객체

    ```js
    let a = {};
    let b = {};

    alert(a == b); // false
    ```

-   객체 복사

    -   `Object.assign` (얕은 복사)
        -   동일한 이름을 가진 프로퍼티가 있으면 기존 값이 덮어씌워진다.

    ```js
    let user = { name: "John" };

    let permissions1 = { canView: true };
    let permissions2 = { canEdit: true };

    Object.assign(user, permissions1, permissions2);

    // user = { name: "John", canView: true, canEdit: true }
    ```

    -   `_.cloneDepp(value)` (깊은 복사)

## 3. 가비지 컬렉션

### 도달가능한(reachable) 값

    -   접근하거나 사용할 수 있는 값
    -   메모리에서 삭제되지 않는다.
    -   태생부터 도달 가능한 값들 (root)
        -   현재 함수의 지역변수와 매개변수
        -   중첩 함수의 체인에 있는 함수에서 사용되는 변수와 매개변수
        -   전역변수
    -   root가 참조하는 값이나 체이닝으로 루트에서 참조할 수 있는 값
    -   도달할 수 없는 객체들은 가비지 컬렉터에 의해 삭제됨

## 4. 메서드와 this

### 메서드

-   객체에 할당된 함수

### this

-   메서드에서 현재 객체에 접근하는 키워드

```js
let user = {
    name: "John",
    age: 30,

    sayHi() {
        alert(this.name);
    },
};

user.sayHi(); // John
```

-   `this` 값은 런타임에 결정된다.

    -   `this`는 점 앞의 객체를 참조함

    ```js
    let user = { name: "John" };
    let admin = { name: "Admin" };

    function sayHi() {
        alert(this.name);
    }

    user.f = sayHi;
    admin.f = sayHi;

    user.f();
    admin.f();
    ```

## 5. 생성자 함수

-   construction function

    -   함수 이름의 첫글자는 대문자로 시작한다.
    -   반드시 `new` 연산자를 붙여 실행한다.

    ```js
    function User(name) {
        // 빈 객체 생성 this = {}
        this.name = name;
        this.isAdmin = false;
        // return this (암시적 반환)
    }

    let user = new User("보라");
    ```

    -   생성자에 return문이 있는 경우
        -   객체를 return하면 객체가 반환됨
        -   원시형을 return하면 return문이 무시되고 this가 반환됨
        ```js
        function BigUser() {
            this.name = "원숭이";
            return { name: "고릴라" }; // 객체 return
        }
        alert(new BigUser().name); // 고릴라
        ```
        ```js
        function BigUser() {
            this.name = "원숭이";
            return "고릴라"; // 원시형 return
        }
        alert(new BigUser().name); // 원숭이
        ```

-   익명 생성자 함수

    -   단 한번만 호출하여 사용할 때 사용

    ```
    let user = new function () {
        this.name = "보라";
        this.isAdmin = false;
    };
    ```

### `new.target`

-   함수가 `new` 키워드로 호출되었으면 함수 자체를 반환한다.
-   일반적인 방식으로 호출되었으면 `undefine`을 반환한다.

```js
function User() {
    alert(new.target);
}
```
