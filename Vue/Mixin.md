### Minxin 이란 ?

믹스인은 이름이 나타내고 있는 것 처럼 컴포넌트에 무언가를 섞어 원하는 것을 구현하는 기능입니다. 믹스인을 구현하고 동작시키는 과정을 순서대로 쓰면 아래와 같이 정리할 수 있습니다.

1. 믹스인할 객체를 만들고
2. 컴포넌트에 객체를 믹스인하고
3. 나머지 부분을 구현해 완성한다

여기서 가장 중요한 '2. 컴포넌트에 객체를 믹스인하고' 과정에서는 아래와 같은 (그림에 시각화해둔) 원칙들이 적용됩니다.

![](https://images.velog.io/images/bongjoki/post/c22f81db-0974-4f84-b674-98c23238bddc/Untitled.png)

### 특징

1.  HTML/CSS는 믹스인하지 않습니다. 즉, 믹스인 파일은 순수 자바스크립트로 작성된 객체입니다.

```javasciprt
   // 가능하긴 하지만 권장되지 않음!
let mixin = {
   ...
   Template: `<div> ...</div>`
   data {
    return {
      styleObj: { 'width' : 100 }
    }
  }
}
```

2. 믹스인에서 선언한 속성(e.g. data, lifecycle hook, methods ...)를 컴포넌트에서 다시 선언할 수 있으며, 이 경우 컴포넌트에 선언된 값을 우선하여 병합됩니다.

```javascript
// 즉, 아래와 같이 mixin.js와 component.vue에 같은 속성이 중복 선언된 경우에
// mixin.js
...
data {
  return {
    age: 20
  }
}
...

// component.vue
  ...
data {
  return {
    age: 26
  }
}
...

// 컴포넌트의 선언값이 살아남습니다.
// result
  <div>{{ age }}</div>
// => <div>26</div>
```

### 예제

#### @/mixins/MyMixin.js

#### @/components/MixinComponent.vue

<iframe src="https://codesandbox.io/embed/vue-mixin-x2xi3?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Vue Mixin"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

### 참조

[Vue.js Mixin: 기능 캡슐화하기](https://velog.io/@bluestragglr/Vue.js-Mixin-%EA%B8%B0%EB%8A%A5-%EB%B0%98%EB%B3%B5-%EC%A0%9C%EA%B1%B0%ED%95%98%EA%B8%B0)
