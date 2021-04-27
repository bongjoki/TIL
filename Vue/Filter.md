### Vue Filter

컴포넌트의 텍스트를 형식화하여 적용할 수 있도록 Vue에서 지원하는 기능.

-   ### 표현법

```html
<template>
    <div>
        <!-- 중괄호 보간법 -->
        <div>{{ name | capitalize }}</div>
        <!-- v-bind 표현 -->
        <div v-bind:name="name | capitalize"></div>
    </div>
</template>
<script>
    export default {
        name: "FilterExample",
        data() {
            return {
                name: "john",
            };
        },
        filters: {
            capitalize: function (value) {
                if (!value) return "";
                value = value.toString();
                return value.charAt(0).toUpperCase() + value.slice(1);
            },
        },
    };
</script>
```

-   ### 전역 Filter 등록
    규모가 큰 프로젝트의 경우 하나의 filter.js 파일을 만들고 전역 필터로 정의하여 어느 vue 파일에서나 불러오도록 사용합니다. 방법은 아래와 같습니다.

**filter.js**

```javascript
//  plugins/filters.js
//  NPM
import Vue from "vue";

Vue.filter("capitalize", function (value) {
    if (!value) {
        return "";
    }
    value = value.toString();
    return value.charAt(0).toUpperCase() + value.slice(1);
});
```

1. Vue
   **src/main.js**

```javascript
import "@/helpers/filters";
//  ...
```

2. Nuxt
   **nuxt.config.js**

```javascript
module.exports = {
    plugins: [{ src: "@/plugins/filters.js" }],
};
```

-   ### 필터 체이닝
    price인자를 comma 받아 실행하고 나온 값을 dollar가 받아 실행 후 리턴합니다.

```html
<template> {{ price | comma | dollar }} </template>
```

-   ### Multi argument
    필터는 기본적으로 js 함수이기에 두개이상의 인자를 받을 수 있습니다.

```
<template>
  {{ price | comma(arg1, arg2) }}
</template>
```

> -   [Vue Filter](https://kr.vuejs.org/v2/guide/filters.html)

-   [vue filter 사용법
    ](https://kyounghwan01.github.io/blog/Vue/vue/filter/)
