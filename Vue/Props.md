# Vue Props

### camelCase vs kebab-case

**JavaScript : camelCase**

```javascript
Vue.component("child", {
    props: ["myMessage"],
    template: "<span>{{ myMessage }}</span>",
});
```

**HTML : kebab-case**

```html
<child my-message="test"></child>
```

### 객체의 모든 속성 prop으로 전달

인자 없이 `v-bind`를 이용하면 객체의 모든 속성을 prop으로 전달할 수 있다.

**예제**
**data()**

```javascript
todo: {
  text: 'Learn Vue',
  isComplete: false
}
```

**`v-bind` 이용**

```html
<todo-item v-bind="todo"></todo-item>
```

아래의 코드는 위의 코드와 동일한 동작을 합니다.

```html
<todo-item
    v-bind:text="todo.text"
    v-bind:is-complete="todo.isComplete"
></todo-item>
```

### 리터럴을 prop으로 전달

> Wiki : [리터럴과 상수](https://velog.io/@bongjoki/%EB%A6%AC%ED%84%B0%EB%9F%B4%EA%B3%BC-%EC%83%81%EC%88%98)

**Bad **
string "1"을 전달

```html
<comp some-prop="1"></comp>
```

**Good**
number "1"을 전달

```html
<comp v-bind:some-prop="1"></comp>

<!-- v-bind를 생략하여, 아래 처럼 표기 가능 -->
<comp :some-prop="1"></comp>
```

### 단방향 데이터 흐름

모든 props는 하위 속성과 상위 속성 사이의 **단방향** 바인딩을 형성합니다. 상위 속성이 업데이트되면 하위로 흐르게 되지만 그 반대는 안됩니다. 이렇게하면 하위 컴포넌트가 실수로 부모의 상태를 변경하여 앱의 데이터 흐름을 추론하기 더 어렵게 만드는 것을 **방지할 수** 있습니다.

#### 단방향 데이터 흐름을 해치지 않는 방법

**1. prop의 초기 값을 로컬 데이터로 지정합니다.**

```javascript
props: ['initialCounter'],
data: function () {
  return { counter: this.initialCounter }
}
```

**2. prop 값으로 부터 계산된 속성을 정의합니다.**

```javascript
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size.trim().toLowerCase()
  }
}
```

### prop 검증

컴포넌트가 받는 중인 **prop에 대한 요구사항**을 지정할 수 있습니다. **요구사항이 충족 되지 않으면 Vue에서 경고**를 내보냅니다. 이 기능은 다른 사용자가 사용할 컴포넌트를 제작할 때 특히 유용합니다.

props를 문자열 배열로 정의하는 대신 **`유효성 검사 요구사항이 있는 객체`**를 사용할 수 있습니다.

```javascript
props: {
	status: {
      	// 데이터 타입 확인
    	type: String,
        // 필요한 prop인지
        required: true,
        // 기본 값 설정
        default: "good",
        // 유효한 value인지 확인
        validator: (status) => ['sad', 'happy','bored', 'good'].indexOf(status) !== -1,
    }
}
```

> [Vue 공식문서 - Props](https://kr.vuejs.org/v2/guide/components.html#Props)
