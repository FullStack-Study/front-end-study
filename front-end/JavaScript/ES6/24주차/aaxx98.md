# 자료구조와 자료형

## 4. 배열

-   순서가 있는 컬렉션
-   생성 및 선언

    ```js
    //생성
    let arr = new Array();
    let arr = [];
    //선언
    let;
    ```

    -   `new Array()`

        -   숫자 인수를 넣어 선언하면 배열의 요소가 모두 `undefinded`로 초기화된다.

            ```js
            let arr = new Array(2);
            alert(arr[0]); // undefined
            alert(arr.length); // 2
            ```

        -   배열 요소를 인수로 넘길수도 있다.

            ```js
            let arr = new Array("사과", "배", "기타"); // ["사과", "배", "기타"]가 생성됨
            ```

-   배열 요소의 자료형에는 제약이 없음
    ```js
    let arr = [
        "사과",
        { name: "이보라" },
        true,
        function () {
            alert("안녕하세요.");
        },
    ];
    alert(arr[1].name);
    arr[3]();
    ```
-   trailing 쉼표 사용 가능
    -   배열 마지막 요소에 쉼표를 붙일 수 있음

### pop/push, shft/unshift

-   `push`: 맨끝에 요소 추가
-   `pop`: 제일 끝 요소 제거, 제거한 요소 반환
-   `shift`: 제일 앞 요소를 꺼내 제거, 제거한 요소 반환
-   `unshift`: 제일 앞에 요소 추가
-   push/pop은 빠르지만 shift/unshift는 요소가 이동하는데 걸리는 시간이 필요하다.

### 배열 내부 동작 원리

-   배열은 객체형에 속함

    -   참조를 통해 복사된다.
    -   프로퍼티를 추가할 수 있다.

-   배열은 내붖적으로 배열 요소를 인접한 메모리 공간에 차례대로 저장되어 연산 속도를 높인다.
    -   배열을 잘못 하용하는 경우
        -   숫자 값이 아닌 프로퍼티 키로 사용하는 경우
            -   ex) `arr.test = 5`
        -   0번째 요소와 1000번째 요소만 추가하는 경우
            ```js
            arr[0] = 1;
            arr[1000] = 1;
            ```
        -   요소를 역순으로 채우는 경우
            ```js
            arr[1000] = 1;
            arr[999] = 1;
            ```

### 반복문

-   `for`문

    ```js
    for (let i = 0; i < arr.length; i++) {
        alert(arr[i]);
    }
    ```

-   `for..of`

    ```js
    for (let fruit of fruits) {
        alert(fruit);
    }
    ```

    -   인덱스는 얻을 수 없다.

-   `for..in`
    -   배열은 객체형이므로 `for..in`으로 순회할 수 있다.
    -   key가 숫자가 아닌 프로퍼티도 순회 대상에 포함되므로 배열의 의도와 맞지 않게 동작할 수 있다.
    -   브라우저나 기타 호스트 환경에서 쓰이는 객체 중, 유사 배열을 대상으로 순회가 이루어질 수 있다.

### length

-   배열 내 가장 큰 index에 1을 더한 값

    ```js
    let fruits = [];
    fruits[123] = "사과";

    alert(fruits.length); // 124
    ```

-   `length`는 쓰기가 가능하다.
    -   큰 값을 할당사면 아무일도 일어나지 않는다.
    -   값을 감소시키면 배열이 잘린다.
        -   `arr.length=0`으로 간단하게 배열을 비울 수 있다.

### 다차원 배열

```js
let matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
];

alert(matrix[1][1]); // 5, 중심에 있는 요소
```

### toString

-   `toString()` 메서드가 구현되어있어 배열 요소를 쉼표로 구분한 문자열로 출력할 수 있다.
    ```js
    let arr = [1, 2, 3];
    alert(arr); // 1,2,3
    ```

## 5. 배열과 메서드

### 요소 추가/제거 메서드

-   push/pop/shift/unshift
-   splice

    -   배열에서 요소 제거, 제거한 요소 배열 반환

    ```js
    let arr = ["I", "study", "JavaScript"];
    let removed = arr.splice(1, 1); // 인덱스 1부터 요소 한 개를 제거
    alert(arr); // ["I", "JavaScript"]
    alert(removed); // ["study"] 삭제한 원소 반환
    ```

    -   제거한 자리에 요소 추가
        -   두 번째 인자 `deleteCount`를 `0`으로 설정하면 요소를 제거하지 않으면서 새로운 요소를 추가할 수 있다.

    ```js
    let arr = ["I", "study", "JavaScript", "right", "now"];
    arr.splice(0, 3, "Let's", "dance"); // index 0부터 3개 요소 삭제 후 ,요소 추가
    alert(arr); // ["Let's", "dance", "right", "now"]
    ```

-   slice

    -   arr.slice([start], [end])
    -   start 인덱스부터 end 이전 인덱스 요소까지 복사한 새로운 배열을 반환한다.
    -   인수를 하나도 넘기지 않으면 배열의 복사본을 만들 수 있다.

-   concat

    -   arr.concat(arg1, arg2...)
    -   배열에 요소를 합친다.

        -   인수가 배열인 경우, 배열의 모든 요소를 복사하여 arr에 추가한다.
        -   인수가 단순 값인 경우 복사하여 arr에 추가한다.
            ```js
            let arr = [1, 2];
            alert(arr.concat([3, 4], 5, 6)); // 1,2,3,4,5,6
            ```
        -   객체인 경우 객체를 통째로 복사하여 arr에 추가한다.
        -   유사배열 객체에 특수한 프로퍼티 `Symbol.isConcatSpreadable`이 있으면 객체 프로퍼티 값이 복사된다.

            ```js
            let arr = [1, 2];
            let arrayLike = {
                0: "something",
                1: "else",
                [Symbol.isConcatSpreadable]: true,
                length: 2,
            };
            alert(arr.concat(arrayLike)); // 1,2,something,else
            ```

### forEach

```js
["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
    alert(`${item} is at index ${index} in ${array}`);
});
```

-   모든 요소 각각에 대해 실행할 함수를 인자로 넘긴다.

### 요소 검색

-   `indexOf(item, from)`: from에서 부터 item요소를 찾는다.
    -   찾으면 해당 요소의 index를 반환한다.
    -   찾지 못하면 -1을 반환한다.
-   `lastIndexOf(item, from)`: indexOf와 동일한 동작을 하는데, 검색을 끝에서 부터 시작한다.
-   `includes(item, from)`: from부터 item요소를 찾는데, 요소를 발견하면 true를 반환한다.
-   `includes`는 `NaN` 처리가 가능하다.
    ```js
    const arr = [NaN];
    alert(arr.indexOf(NaN)); // -1
    alert(arr.includes(NaN)); // true
    ```

### 객체 검색

-   find

    ```js
    let result = arr.find(function (item, index, array) {
        // true가 반환되면 반복이 멈추고 해당 요소를 반환
        // 조건에 해당하는 요소가 없으면 undefined를 반환
    });
    ```

    -   item: 함수를 호출할 요소
    -   index: 요소의 인덱스
    -   array: 배열 자기 자신
    -   모든 요소에 대해 함수가 실행된다.
        -   함수가 참을 반환하면 탐색이 중단되고 해당 요소가 반환된다.
        -   참이 한번도 반환되지 않으면 undefinded가 반환된다.

-   findIndex

    -   find와 동일하나, 조건에 맞는 요소를 만환하는 대신 index를 반환한다.
    -   조건에 맞는 요소가 없으면 -1을 반환한다.

-   filter
    -   조건을 충족하는 여러개의 요소를 찾아서 배열로 반환한다.

### 배열 변형

-   map

    -   배열 요소 전체를 대상으로 함수를 호출하고, 함수 호출 결과를 배열로 반환해준다.

-   sort

    -   배열 요소 정렬, 배열이 변경된다.
    -   모든 요소는 문자열로 취급되어 재정렬된다.
        ```js
        let arr = [1, 2, 15];
        arr.sort();
        alert(arr); // 1, 15, 2
        ```
    -   새로운 정렬 기준을 함수로 넘겨줄 수 있다.

        ```js
        function compareNumeric(a, b) {
            if (a > b) return 1;
            if (a == b) return 0;
            if (a < b) return -1;
        }

        let arr = [1, 2, 15];
        arr.sort(compareNumeric);
        alert(arr); // 1, 2, 15
        ```

-   reverse

    -   배열 요소 역순으로 정렬

-   split
    -   문자열 -> 배열
-   join
    -   배열 -> 문자열
-   reduce

    -   배열을 기반으로 값하나를 도출

    ```js
    let arr = [1, 2, 3, 4, 5];
    let result = arr.reduce((sum, current) => sum + current, 0); // 초기값 0
    alert(result); // 15
    ```

    -   reduce(func([이전 함수의 반환값],[현재 순회 요소]), [초기값])
        -   초기값을 명시하지 않으면 배열 첫번째 값이 초기값이 되고, 두번째 요소부터 함수가 실행된다.

-   reduceRight
    -   reduce와 비슷하지만 배열의 끝부터 연산을 수행한다.

### Array.isArray

-   배열은 객체형으로 취급되어 `typeof`로 객체와 배열을 구분하기 어렵다.
    ```js
    alert(Array.isArray({})); // false
    alert(Array.isArray([])); // true
    ```

### thisArg

-   배열 메서드 사용시, 객체 내의 메소드를 인자로 넘겨주고, 메소드에 대한 `this` 객체를 지정한다.

    -   거의 모든 배열 메서드에서 사용 가능하다. (sort 제외)

    ```js
    let army = {
        minAge: 18,
        maxAge: 27,
        canJoin(user) {
            return user.age >= this.minAge && user.age < this.maxAge;
        },
    };

    let users = [{ age: 16 }, { age: 20 }, { age: 23 }, { age: 30 }];

    let soldiers = users.filter(army.canJoin, army);

    alert(soldiers.length); // 2
    alert(soldiers[0].age); // 20
    alert(soldiers[1].age); // 23
    ```

## 6. iterable 객체

-   _iterable: 반복가능한_
-   iterable 객체는 배열을 일반화한 객체이다.
-   iterable 객체는 `for..of`를 사용할 수 있다.
    -   iterable에는 메서드 `Symbol.iterator`가 구현되어 있다.
    -   `for..of` 실행 시 `Symbol.iterator`가 호출된다.
    -   obj[Symbol.iterabor]의 결과는 iterator이다.
        -   이터레이터는 반복 과정을 처리한다.
        -   이터레이터에는 객체 `{done: Boolean, value: any}`를 반환하는 next() 메서드가 구현되어있다.
            -   done: 반복이 끝나면 true

```js
let range = {
    from: 1,
    to: 5,
};

// Symbol.iterator는 next 메소드를 가진 이터레이터 객체를 반환한다.
range[Symbol.iterator] = function () {
    return {
        current: this.from,
        last: this.to,

        //반복마다 next()가 호출된다. done, value를 가진 객체를 반환한다.
        next() {
            if (this.current <= this.last) {
                return { done: false, value: this.current++ };
            } else {
                return { done: true }; // {done:true}가 반환되면 더이상 next는 호출되지 않는다.
            }
        },
    };
};

for (let num of range) {
    alert(num); // 1, 2, 3, 4, 5
}
```

-   문자열은 이터러블이다.

### 유사배열과 이터러블

-   유사배열: `length` 프로퍼티가 있어 배열처럼 보이는 객체

    ```js
    let arrayLike = {
        0: "Hello",
        1: "World",
        length: 2,
    }; // 이터레이터가 구현되어있지 않으므로 for..of 순회는 불가능하다.
    ```

-   이터러블과 유사배열은 배열이 아니므로 배열 메소드를 지원하지 않는다.

### Array.from

-   이터러블이나 유사배열을 받아 Array로 만들어준다.

    ```js
    let arrayLike = {
        0: "Hello",
        1: "World",
        length: 2,
    };

    let arr = Array.from(arrayLike);
    alert(arr.pop()); // World

    arr = Array.from(range);
    alert(arr); // 1,2,3,4,5
    ```

## 7. 맵과 셋

### 맵

-   key가 있는 데이터를 저장한다. 객체와 달리 key는 다양한 자료형이 될 수 있다.
    -   객체를 key로 가질 수 있다.
    -   NaN도 key로 사용될 수 있다.

### 주요 메서드와 프로퍼티

-   `new Map()`: 생성자
-   `set(key, value)`: key-value 생성하여 저장
    -   맵 자신이 반환된다. map.set을 체이닝하여 사용할 수 있다.
    ```js
    map.set("1", "str1").set(1, "num1").set(true, "bool1");
    ```
-   `get(key)`: key값을 가진 value 반환, 없으면 `undefinded` 반환
-   `has(key)`: key가 존재하면 `true`, 아니면 `false` 반환
-   `delete(key)`: key에 해당하는 value 삭제
-   `clear()`: 맵의 모든 요소 제거
-   `size`: 맵의 요소 개수 반환

### 맵의 요소에 반복 작업하기

-   맵은 삽입된 순서대로 순회가 일어난다.
-   `keys()`: 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환
-   `values()`: 각 요소의 값을 모은 이터러블 객체를 반환
-   `entries()`: 요소의 [키, 값]을 한 쌍으로 하는 이터러블 객체를 반환
    -   맵 `for..of` 순회와 동일하다.

```js
let recipeMap = new Map([
    ["cucumber", 500],
    ["tomatoes", 350],
    ["onion", 50],
]);

for (let vegetable of recipeMap.keys()) {
    alert(vegetable); // cucumber, tomatoes, onion
}

for (let amount of recipeMap.values()) {
    alert(amount); // 500, 350, 50
}

for (let entry of recipeMap) {
    alert(entry);
    // cucumber,500
    // tomatoes,350
    // onion,50
}
```

### Object.fromEntries

-   맵을 일반 객체로 바꿔준다.

    ```js
    let map = new Map();
    map.set("banana", 1);
    map.set("orange", 2);
    map.set("meat", 4);

    let obj = Object.fromEntries(map.entries());
    // obj = { banana: 1, orange: 2, meat: 4 }

    alert(obj.orange); // 2
    ```

### 셋

-   Set은 중복을 허용하지 않는 컬렉션이다.

### 주요메소드와 프로퍼티

-   `new Set(iterable)`: 생성자, 이터러블 객체를 받으면 요소를 복사하여 셋에 넣어준다.
-   `add(value)`: 값을 추가하고 셋 자신을 반환
-   `delete(value)`: 값 제거, 제거에 성공하면 `true` 반환
-   `has(value)`: 값이 있으면 `true` 반환, 없으면 `false` 반환
-   `clear()`: 셋의 모든 요소 제거
-   `size`: 셋의 요소 개수 반환

-   `for..of`, `forEach`로 반복작업 수행 가능
-   맵처럼 `keys()`, `values()`, `entries()` 메소드를 가진다.
    -   `entries`는 value-value 쌍을 반환한다. (맵과의 호환성 때문)
