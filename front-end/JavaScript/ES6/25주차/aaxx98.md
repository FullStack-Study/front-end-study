## 5.8 위크맵과 위크셋

### 위크맵(WeakMap)

-   맵과 위크맵

    -   맵의 키를 객체로 설정하고 객체 참조에 null을 할당해도 객체는 가비지컬렉션에 의해 메모리에서 삭제되지 않는다.
    -   위크맵의 키로 사용된 객체를 참조하고 있는 변수가 아무것도 없다면 해당 객체는 가비지컬렉션에 의해 메모리에서 삭제된다.

        ```js
        let john = { name: "John" };

        let weakMap = new WeakMap();
        weakMap.set(john, "...");

        john = null;
        ```

    -   위크맵은 반드시 키가 객체여야한다.
    -   원시값은 위크맵의 키가 될 수 없다.

-   위크맵 메소드
    -   `get(key)`
    -   `set(key, value)`
    -   `delete(key)`
    -   `has(key)`
    -   반복 작업과 `keys()`, `values()`, `entries()`는 지원하지 않는다.
        -   가비지컬렉션의 동작시점을 정확히 알 수 없기 때문에 위크맵 전체 요소에 대한 메소드를 지원하지 않는다.

### 위크맵 사용 예시: 추가 데이터

-   부차적인 데이터를 저장할 곳이 필요할 때 사용한다.
-   ex) 객체가 살아있는 동안만 유효한 데이터 `[객체:데이터]`

    ```js
    let visitsCountMap = new Map(); // [사용자:방문횟수]를 저장하는 맵

    // 사용자가 방문하면 방문 횟수를 1 늘림
    function countUser(user) {
        let count = visitsCountMap.get(user) || 0;
        visitsCountMap.set(user, count + 1);
    }

    // 사용자가 방문했을 때
    let john = { name: "John" };
    countUser(john);

    // 사용자가 삭제될 때
    john = null;
    ```

    -   사용자 객체가 사라지면 방문 횟수도 삭제된다.

### 위크맵 사용 예시: 캐싱

-   동일한 함수를 여러번 호출해야 할 때
-   최초 호출 시 반환된 값을 저장해놓고, 함수 호출 대신 사용할 때

```js
let cache = new WeakMap();

function process(obj) {
    if (!cache.has(obj)) {
        // 최초 호출
        let result = /* 연산 수행 */ obj;

        cache.set(obj, result);
    }

    return cache.get(obj);
}

let obj = {
    /* ... 객체 ... */
};

let result1 = process(obj);
let result2 = process(obj);

// 객체 삭제
obj = null;
```

### 위크셋(WeakSet)

-   객체만 저장 가능, 원시값은 저장할 수 없음
-   셋 안의 객체는 도달 가능할 때만 메모리에 유지됨
-   워크셋 메서드

    -   `add(obj)`
    -   `has(obj)`
    -   `delete(obj)`
    -   반복 작업과 `keys()`, `values()`, `entries()`는 지원하지 않는다.

-   부차적인 데이터 저장시 사용

```js
let visitedSet = new WeakSet(); // 방문자를 저장하는 위크셋

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

visitedSet.add(john); // John 방문
visitedSet.add(pete); // Pete 방문
visitedSet.add(john); // John 방문

// 방문여부 확인
alert(visitedSet.has(john)); // true
alert(visitedSet.has(mary)); // false

// 죽은 방문자는 확인하지 않음
john = null;
```

## 5.9 Object.keys, values, entries

-   keys, values, entries (순회 관련)메소드를 사용할 수 있는 자료구조

    -   Map, Set, Array
    -   `map.keys()`와 같이 사용, iterable 객체 반환

-   일반 객체 순회
    -   `Object.keys(obj)`
    -   `Object.values(obj)`
    -   `Object.entries(obj)`
    -   배열 반환

### 객체 변환하기

-   객체에서 map, filter와 같은 객체 전용 메소드를 사용하려면,
    `Object.entries`와 `Object.fromEntries`를 순차적으로 적용해야 함

    -   1. `Object.entries(obj)`를 사용해 객체의 키-값 쌍이 요소인 배열을 얻는다.
    -   2. 만든 배열에 `map`과 같은 배열 전용 메소드를 적용한다.
    -   3. 반환된 배열에 `Object.fromEntries(array)`를 적용해 배열을 다시 객체로 되돌린다.

        ```js
        let prices = {
            banana: 1,
            orange: 2,
            meat: 4,
        };

        let doublePrices = Object.fromEntries(
            Object.entries(prices).map(([key, value]) => [key, value * 2])
        );

        alert(doublePrices.meat); // 8
        ```

## 5.10 구조 분해 할당

### 배열 분해

```js
let arr = ["Bora", "Lee"];
let [firstName, surname] = arr;
alert(firstName); // Bora
alert(surname); // Lee
```

-   할당 연산자 오른쪽에는 모든 이터러블이 올 수 있다.

    ```js
    let [a, b, c] = "abc"; // ["a", "b", "c"]
    let [one, two, three] = new Set([1, 2, 3]);
    ```

-   요소 무시하기

    ```js
    let [firstName, , title] = [
        "Julius",
        "Caesar",
        "Consul",
        "of the Roman Republic",
    ];
    alert(title); // Consul
    ```

-   변수 교환

```js
let guest = "Jane";
let admin = "Pete";

[guest, admin] = [admin, guest];
// guest => "Pete"
// admin => "Jane"
```

-   나머지 값들 가져오기
    -   `...`

```js
let [name1, name2, ...rest] = [
    "Julius",
    "Caesar",
    "Consul",
    "of the Roman Republic",
];

alert(name1); // Julius
alert(name2); // Caesar

// rest = ["Consul", "of the Roman Republic",]
```

-   기본값

    -   변수 개수가 배열 길이보다 커서 할당할 값이 없으면 undefinded가 할당된다.
    -   기본값 설정하기

        ```js
        // 기본값
        let [name = "Guest", surname = "Anonymous"] = ["Julius"];
        alert(name); // Julius
        alert(surname); // Anonymous
        ```

### 객체 분해

```js
let options = {
    title: "Menu",
    width: 100,
    height: 200,
};

let { title, width, height } = options;

alert(title); // Menu
alert(width); // 100
alert(height); // 200
```

-   순서는 상관 없다.
-   프로퍼티 키와 다른 이름의 변수로 저장하기

    ```js
    // { 객체 프로퍼티: 목표 변수 }
    let { width: w, height: h, title } = options;

    alert(title); // Menu
    alert(w); // 100
    alert(h); // 200
    ```

-   기본값

    ```js
    let options = {
        title: "Menu",
    };

    let { width = 100, height = 200, title } = options;

    alert(title); // Menu
    alert(width); // 100
    alert(height); // 200
    ```

-   나머지값들 가져오기

    ```js
    let options = {
        title: "Menu",
        height: 200,
        width: 100,
    };

    let { title, ...rest } = options;
    //rest = {height: 200, width: 100}
    ```

### 중첩 구조 분해

```js
let options = {
    size: {
        width: 100,
        height: 200,
    },
    items: ["Cake", "Donut"],
    extra: true,
};

let {
    size: { width, height },
    items: [item1, item2],
    title = "Menu",
} = options;

alert(title); // Menu
alert(width); // 100
alert(height); // 200
alert(item1); // Cake
alert(item2); // Donut
```
