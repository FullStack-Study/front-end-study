# 객체

## 4.6 옵셔널 체이닝

-   `?.`

    -   앞 평가 대상이 undefinded나 null이면 평가를 멈추고 undefinded를 반환한다.

        ```js
        let user = {}; // 주소 정보가 없는 사용자
        alert(user?.address?.street); // undefined
        ```

    -   옵셔널 체이닝은 존재하지 않아도 괜찮은 대상에만 사용해야한다.
        -   ex) 필수값이 아닌 것에 사용해야함
            -   user(필수값) 내부의 필수값이 아닌 address의 존재여부를 확인하는 것이 바람직하다.
            -   `user.address?.street`
    -   `?.` 앞의 변수는 반드시 선언되어있어야한다. (선언되지 않으면 에러 발생)
    -   `?.`는 읽기, 삭제하기에 사용할 수 있지만 쓰기에는 사용할 수 없다
        ```js
        user?.name = "Violet";
        ```
        -   user 객체가 없는 경우 `undefinded = "Violet"`이 되어 `SyntaxError: Invalid left-hand side in assignment`가 발생한다.

-   `?.()와 ?.[]`

    -   `?.`는 연산자가 아니라 함수나 대괄호와 함께 동작하는 특별한 문법 구조체이다.

    -   존재여부가 확실하지 않은 함수에서

        ```js
        let user1 = {
            admin() {
                alert("관리자 계정입니다.");
            },
        };

        let user2 = {};

        user1.admin?.(); // user1.admin() 실행
        user2.admin?.(); // user2.admin()이 없어 아무것도 실행하지 않음
        ```

    -   존재여부가 확실하지 않은 프로퍼티에 접근하는 경우

        ```js
        let user1 = {
            firstName: "Violet",
        };
        let user2 = null;

        let key = "firstName";

        alert(user1?.[key]); // Violet
        alert(user2?.[key]); // undefined
        ```

    -   존재여부가 확실하지 않은 프로퍼티를 삭제하는 경우
        ```js
        delete user?.name;
        ```

## 4.7 심볼형

### 심볼

-   심볼은 유일한 식별자를 만들고 싶을 때 사용한다.
-   심볼 값은 `Symbol()`을 사용하여 생성한다. 심볼 이름을 지정할 수도 있다.

    ```js
    // 심볼 생성
    let id = Symbol();
    // 심볼에 심볼 이름 지정
    let id = Symbol("id");
    ```

-   심볼은 유일성이 보장되는 자료형이므로 이름이 동일한 심볼을 여러개 반들어도 각 심볼값이 다르다. 심볼 이름은 어떤 것에도 영향을 주지 않는 이름표 역할만을 한다.

    ```js
    let id1 = Symbol("id");
    let id2 = Symbol("id");

    alert(id1 == id2); // false
    ```

-   심볼은 문자형으로 자동형변환 되지 않는다.

    -   심볼을 출력하고 싶다면 `.toString()`을 사용하거나 `[symbol].description`을 사용하면 된다.

-   `for ... in` 에서 심볼 키를 가진 프로퍼티는 배제된다.
-   `Object.assign`은 키가 심볼인 프로퍼티를 포함하여 객체 내 모든 프로퍼티를 복사한다.

    ```js
    let id = Symbol("id");
    let user = {
        [id]: 123,
    };

    let clone = Object.assign({}, user);

    alert(clone[id]); // 123
    ```

### 숨김 프로퍼티

-   외부 코드에서 접근이 불가능하고 값도 덮어 쓸 수 없는 프로퍼티를 생성할 수 있다.
-   심볼을 프로퍼티 key로 사용한다.

    ```js
    let user = {
        name: "John",
    };

    let id = Symbol("id");
    user[id] = 1;
    alert(user[id]); // 심볼을 키로 사용해 데이터에 접근
    ```

    -   서드파티 코드에서는 `id` 심볼에 접근할 수 없고 `user[id]`에도 접근이 불가능하다.

    -   객체 리터럴에서 심볼형 키는 대괄호로 표현한다.

    ```js
    let id = Symbol("id");

    let user = {
        name: "John",
        [id]: 123, // id: 123은 문자열 키가 된다.
    };
    ```

### 전역 심볼

-   전역 심볼 레지스트리

    -   전역 심볼 레지스트리 내에 심볼을 만들고 해당 심볼에 접근하면, 이름이 같은 경우 동일한 심볼을 반환해준다.
    -   심볼을 읽거나, 새로운 심볼을 반환하려면 `Symbol.for(key)`를 사용하면 된다.

        ```js
        // 전역 레지스트리에서 심볼 읽기
        let id = Symbol.for("id"); // 심볼이 존재하지 않으므로 새로운 심볼을 생성한다.

        // id라는 이름을 가진 심볼이 있으면 반환해준다.
        let idAgain = Symbol.for("id"); // 위에서 생성한 심볼이 반환된다.

        alert(id === idAgain); // true
        ```

    -   전역 심볼의 이름을 얻고싶다면 `Symbol.keyFor`을 사용한다.

        ```js
        let sym = Symbol.for("name");
        let sym2 = Symbol.for("id");

        alert(Symbol.keyFor(sym)); // name
        alert(Symbol.keyFor(sym2)); // id
        ```

### 시스템 심볼

-   자바스크립트 내부에서 사용되는 심볼
-   잘 알려진 심볼
    -   `Symbol.hasInstance`
    -   `Symbol.isConcatSpreadable`
    -   `Symbol.iterator`
    -   `Symbol.toPrimitive`

## 4.8 객체를 원시형으로 변환하기

### ToPrimitive

-   특수 객체 메서드를 사용하면 숫자형이나 문자형으로의 형변환을 원하는대로 조절할 수 있다.
-   hint(형변환을 기대하는 자료형)를 기준으로 객체 형변환은 세 종류가 있다.

    -   1. string
        ```js
        alert(obj); // 객체를 출력할 때
        anotherObj[obj] = 123; // 객체를 프로퍼티 키로 사용할 때
        ```
    -   2. number
        ```js
        let num = Number(obj); // 명시적 형변환
        let n = +obj; // 단항 덧셈 연산
        let delta = date1 - date2; // 뺄셈 연산
        let greater = user1 > user2; // 크기 비교
        ```
    -   3. default

        -   연산자가 기대하는 자료형이 확실하지 않을 때, hint는 default가 된다.
            -   이항 덧셈 연산자 `+`
            -   동등 연산자 `==`

        ```js
        let total = obj1 + obj2;
        if (user == 1) { ... };
        ```

        -   Date 객체를 제외한 모든 내장 객체는 hint가 default인 경우 number인 경우와 동일하게 처리한다.

### 자바스크립트 형변환 알고리즘

-   1. 객체에 `obj[Symbol.toPrimitive](hint)`메서드가 있는지 찾고, 있다면 메서드를 호출
-   2. hint가 `string`이라면
    -   `obj.toString()`이나 `obj.valueOf()`를 호출
-   3. hint가 `number`나 `default`라면
    -   `obj.valueOf()`나 `obj.toString()`을 호출

### Symbol.toPrimitive

-   목표하는 자료형(hint)를 명시하는데 사용한다.

    ```js
    let user = {
        name: "John",
        money: 1000,

        // Symbol.toPrimtive 구현
        // string으로 변환된다면 이름 리턴
        // 아니라면 money 리턴
        [Symbol.toPrimitive](hint) {
            alert(`hint: ${hint}`);
            return hint == "string" ? `{name: "${this.name}"}` : this.money;
        },
    };

    alert(user); // hint: string -> {name: "John"}
    alert(+user); // hint: number -> 1000
    alert(user + 500); // hint: default -> 1500
    ```

### toString과 valueOf

-   형변환을 직접 구현할 수 있다.
-   객체에` Symbol.toPrimitive`가 없으면 `toString`이나 `valueOf`를 호출한다.

    -   hint가 `string`인 경우: `toString` 호출, 없다면 `valueOf` 호출
    -   그 외: `valueOf` 호출, 없다면 `toString` 호출

-   일반 객체의 경우
    -   `toString`: 문자열 "[object Object]" 반환
    -   `valueOf`: 객체 자신을 반환
