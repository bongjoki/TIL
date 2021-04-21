# asyncData()

### 특징

서버사이드 랜더링을 하기 위해 `Nuxt.js`는 컴포넌트 데이터를 세팅하기 전에 비동기 처리를 할 수 있도록 `asyncData()`를 제공한다.

-   `asyncData()`는 컴포넌트(only Page)를 로드하기 전에 호출된다.
-   `asyncData()`는 [컨텍스트](https://ko.nuxtjs.org/docs/2.x/internals-glossary/context/) 객체를 첫번째 인수로 받으며, 이를 사용해 일부 데이터를 가져와 컴포넌트 데이터를 반환할 수 있다.
-   `asyncData()`의 return값은 컴포넌트의 data와 병합된다.

> `asyncData()`는 컴포넌트를 초기화 하기 전에 실행되기 때문에 메서드 내부에서는 this를 통해 컴포넌트 인스턴스에 접근할 수 없다.

### 사용 방법

#### 1. Promise 객체 사용

```javascript
export default {
    asyncData({ params }) {
        return axios.get(`https://my-api/posts/${params.id}`).then((res) => {
            return { title: res.data.title };
        });
    },
};
```

#### 2. async/await 사용

```javascript
export default {
    async asyncData({ params }) {
        const { data } = await axios.get(`https://my-api/posts/${params.id}`);
        return { title: data.title };
    },
};
```

### 참조

> [[TIL] Nuxt.js asyncData 메서드](https://velog.io/@nungsun/TIL-Nuxt.js-asyncData-%EB%A9%94%EC%84%9C%EB%93%9C)
