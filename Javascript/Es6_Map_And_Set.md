# ES6 - Map, Set

### Map

-   `Map()` 은 자바스크립트의 **key-value 페어(pair)** 로 이루어진 컬렉션
-   key 를 사용해서 value 를 get(), set() 할 수 있음
-   key 들은 중복될 수 없음: **하나의 key 에는 하나의 value** 만
-   key 로 사용할 수 있는 데이터형: string, symbol(ES6), object, function >> **number** 는 사용할 수 없음에 주의!

### Object와 비교

-   Object 의 key 는 string 과 symbol(ES6) 만 가능하지만, Map 은 어떤 값도 가능
-   Object 에서는 크기를 추적해서 알 수 있지만, Map 은 손쉽게 얻을 수 있음(size)

#### Map의 set() mehtod로 key, value entry를 추가하는 방법

```javascript
let person = new Map();
me.set("name", "kevin");
me.set("age", 28);
```

#### 대괄호를 사용해서 Map 을 선언하는 방법

```javascript
const person = new Map([
    ["name", "kevin"],
    ["age", 28],
]);
```

#### Method chainning

```javascript
let person = new Map().set("name", "kevin").set("age", 28);
```

#### 그 외 method

```javascript
console.log(you.get("name"));
// 'kevin'
// has(): 주어진 key 가 존재하는지 확인
console.log(me.has("name"));
// true
// size: map 에 담겨진 엔트리의 개수를 조회
console.log(you.size);
// 2
// delete(): 엔트리를 삭제
me.delete("age");
console.log(me.has("age"));
// false
// clear(): 모든 엔트리를 삭제
you.clear();
console.log(you.size);
// 0
```

### Map의 iterable object

-   **`keys()` `values()`**
-   **key** 혹은 **value**들을 순회할 수 있는 iterable object를 반환

#### 예제

```javascript
let me = new Map().set("a", 1).set("b", 2).set("c", 3);
console.log([...me.keys()]); // ['a', 'b', 'c']
console.log([...me.values()]); // [1, 2, 3]
```

-   **`entries()` `next()`** -`Map()` 내부의 모든 요소들을 순회할 수 있는 iterable object를 반환

```javascript
let tripHistory = new Map().set("Seoul", 28).set("Tokyo", 26);
let iterObj = tripHistory.entries();
console.log(iterObj.next()); // {value: ['Seoul', 28], done: false}
console.log(iterObj.next()); // {value: ['Tokyo', 26], done: false}
console.log(iterObj.next()); // {value: undefined, done: true}
```

-   **`for-of` `forEach()`**
-   **`forEach`** 의 경우, 인자 순서가 이상한데(key, value 순서가 반대) Array.prototype.forEach() 구문과 통일성을 유지하기 위함(value, index, array 순서인 것)

```javascript
let devices = new Map().set("macBookPro", 3000).set("iPad", 1200);
// for-of 로 map 순회하기
for (let [key, value] of devices) {
    console.log(key + "^" + value);
}
// 'macBookPro^300', 'iPad^120'
// forEach 로 map 순회하기
we.forEach((value, key, map) => {
    console.log(key + "$" + value);
});
// 'macBookPro$3000', 'iPad$1200'
```

-   자바스크립트 배열 메서드에 존재하는 `map()`, `filter()` 는 Map 에 존재하지 않는다. 하지만 아래와 같은 방식으로 우회해서 사용이 가능하다.

```javascript
let me = new Map().set("a", 1).set("b", 2);
// value 가 1 이상인 엔트리만 filtering 하기
let map1 = new Map([...me].filter(([key, value]) => value > 1));
console.log([...map1.entries()]);
// [['b', 2]]
// key 뒤에 'super' 문자열을 붙이고, value 에 1을 더하기
let map2 = new Map([...me].map(([key, value]) => [key + "super", value + 1]));
console.log([...map2.entries()]);
// [['asuper, 2], [bsuper, 3]]
```

### Set

-   `Set()` 은 value들로 이루어진 컬렉션 (**집합**이라는 표현이 적절)
-   Array 와는 다르게 Set은 같은 value를 2번 이상 포함할 수 없음 (**중복 값 X**)
-   `Set()`의 **`has()` 는 `indexOf()` 보다 빠르다.** 다만, index가 존재하지 않기때문에 index를 이용해서 value로 접근할 수 없다.

#### 예제

```javascript
// 새로운 set 을 만들고 인자로 전달된 iterable 로 인자를 채움
let setB = new Set().add("a").add("b");
setB.add("c");
console.log(setB.size); // 3
// has(): 주어진 값이 set 안에 존재할 경우, true 를 반환
// indexOf() 보다 빠름. 단, index 가 없음
console.log(setB.has("b")); // true
// set 에서 주어진 값을 제거
setB.delete("b");
console.log(setB.has("b")); // false
// set 안의 모든 데이터를 제거
setB.clear();
console.log(setB.size); // 0
```

### Set의 iterable object

-   **`values()`**
-   기본적으로 Set 의 prototype 메서드로 keys() 는 존재하지 않고, values() 만 존재하지만, map 오브젝트와 동일하게 동작하기 때문에 Set.keys() 는 Set.values() 와 같은 결과를 출력한다.

```javascript
let setA = new Set();
setA.add("a");
setA.add("b");
setA.add("a");
console.log([...setA.keys()]); // ['a', 'b']
console.log([...setA.values()]); // ['a', 'b']
```

-   **`entries()`**

```javascript
let countries = new Set();
countries.add("Korea");
countries.add("Japan");
countries.add("China");
let entriesByCountries = countries.entries();
console.log(entriesByCountries.next());
// {value: ['Korea', 'Korea'], done: false}
console.log(entriesByCountries.next());
// {value: ['Japan', 'Japan'], done: false}
console.log(entriesByCountries.next());
// {value: ['China', 'China'], done: false}
console.log(entriesByCountries.next());
// {value: undefined, done: true}
```

-   **`for-of` `forEach`**

```javascript
let countries = new Set();
countries.add("Korea");
countries.add("Japan");
countries.add("China");
for (let country of countries) {
    console.log(country);
}
// 'Korea', 'Japan', 'China'
countries.forEach((value, key) => {
    console.log(value);
});
// Korea', 'Japan', 'China'
```

### Set : 집합 연산

![스위프트 집합 연산](https://miro.medium.com/max/700/1*Zp0Ksu7UeJbApAnyVy_mTQ.png)

```javascript
let setA = new Set([1, 2, 3, 4, 5]);
let setB = new Set([4, 5, 6, 7, 8]);
```

-   합집합 (union)

```javascript
let unionSet = new Set([...setA, ...setB]);
for (let value of unionSet) {
    console.log(value);
}
// 1, 2, 3, 4, 5, 6, 7, 8
```

-   교집합 (intersection)

```javascript
let intersectionSet = new Set([...setA].filter((v) => setB.has(v)));
for (let value of intersectionSet) {
    console.log(value);
}
// 4, 5
```

-   차집합 (difference)

```javascript
let differenceSet = new Set([...setA].filter((v) => !setB.has(v)));
for (let value of differenceSet) {
    console.log(value);
}
// 1, 2, 3
```

-   대칭 차집합(symmetricDifference)

```javascript
var symmetricDifferenceSet = new Set([
    ...[...setA].filter((x) => !setB.has(x)),
    ...[...setV].filter((x) => !setA.has(x)),
]);
for (let value of symmetricDifferenceSet) {
    console.log(value);
}
// 1, 2, 3, 6, 7, 8
```

### 참조

> [[JS #5] ES6 Map(), Set()](https://medium.com/@hongkevin/js-5-es6-map-set-2a9ebf40f96b)
