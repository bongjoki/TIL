# 배열 중복 요소 제거하는 3가지 방법

## 목록

```
  1. Set()
  2. indexOf(), filter()
  3. forEach(), includes()
```

### 1. Set

Javascript에서 `Set` 객체를 이용하면 중복없는 데이터를 표현할 수 있습니다.
`Set` 객체의 이런 특징을 이용해서, 배열의 중복을 제거할 수 있습니다.

```javascript
const dupArr = [1, 2, 3, 1, 2];

const set = new Set(dupArr);

const uniqueArr = [...set];
```

### 2. indexOf(), filter()

`indexOf()` 함수는, 배열에서 특정값이 처음으로 나타나는 index를 리턴합니다.
`filter()` 함수는 특정 조건에 부합하는 배열의 모든 값을 배열 형태로 리턴합니다.
이 두 함수를 사용하여 배열에 중복된 값을 제거 할 수 있습니다.

```javascript
const dupArr = [1, 2, 3, 1, 2];

const uniqueArr = dupArr.filter((element, index) => {
    return dupArr.indexOf(element) === index;
});

document.writeln(Array.isArray(uniqueArr));
document.writeln(uniqueArr);
```

### 3. forEach(), includes()

`forEach()` 함수는 주어진 배열을 순회하면서, 배열의 원소들로 주어진 callback함수를 실행합니다.
`include()` 함수는 주어진 배열에 특정 값이 포함되는지 여부를 검사합니다.

```javascript
const dupArr = [1, 2, 3, 1, 2];

let uniqueArr = [];
dupArr.forEach((element) => {
    if (!uniqueArr.includes(element)) {
        uniqueArr.push(element);
    }
});

document.writeln(Array.isArray(uniqueArr));
document.writeln(uniqueArr);
```

## 참조

[[Javascript] 배열 중복 제거하는 3가지 방법](https://hianna.tistory.com/422)
