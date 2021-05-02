# Vue Slot

### Slot에 들어가는 내용

슬롯(slot)은 컴포넌트의 재사용성을 높여주는 기능입니다. 특정 컴포넌트에 등록된 하위 컴포넌트의 마크업을 확장하거나 재정의할 수 있습니다. 바로 코드로 살펴보겠습니다.

**index.vue**

```javascript
<navigation-link url="/profile">Your Profile</navigation-link>
```

그리고 `<navigation-link>` 템플릿을 아래와 같이 만들 수 있습니다.

**NavigationLink.vue**

```javascript
<a v-bind:href="url" class="nav-link">
    <slot></slot>
</a>
```

컴포넌트를 렌더링할 때 <slot></slot>이 부분이 `<navigation-link>`의 innerHTML이 “Your Profile”로 교체됩니다. 다음과 같이 컴파일 됩니다.
**index.vue**

```javascript
<a v-bind:href="/profile" class="nav-link">
    Your Profile
</a>
```

다음과 같이 HTML 템플릿 컴포넌트`<font-awesome-icon>`도 가능합니다.
**index.vue**

```javascript
<navigation-link url="/profile">
  <!-- 컴포넌트로 아이콘을 추가해봅시다 -->
  <font-awesome-icon name="user"></font-awesome-icon>
</navigation-link>
```

다음과 같이 컴파일 됩니다.
**index.vue**

```javascript
<a v-bind:href="/profile" class="nav-link">
    <font-awesome-icon name="user"></font-awesome-icon>
</a>
```

### 컴파일될 때의 범위

슬롯 안에 데이터 옵션을 사용하고 싶을 수 있습니다. 아래의 예를 봅시다.

**index.vue**

```javascript
<navigation-link url="/profile">
  Logged in as {{ user.name }}
</navigation-link>
```

여기서 슬롯은 같은 템플릿의 나머지와 똑같은 인스턴스 속성(즉 같은 “범위”)에 연결되어 있습니다. 슬롯이 <navigation-link>의 범위에 연결된 것이 아닌 거죠. 예를 들어 url에 접근하려고 하면 작동하지 않을 것입니다.

**index.vue**

```javascript
<navigation-link url="/profile">
Clicking here will send you to: {{ url }}
<!--
url은 부모 컴포넌트의 인스턴스 이므로 undefined로 나올 겁니다.
이 데이터는 <navigation-link>로 넘어가지만
<navigation-link> 컴포넌트 안에 정의되어 있지는
않으니까요.
-->
</navigation-link>
```

> 💡 **부모 템플릿 안에 있는 것들은 부모 컴포넌트의 범위에 컴파일되고 자식 템플릿 안에 있는 것들은 자식 컴포넌트의 범위에 컴파일됩니다.**

### 참조

> [Vue.js 컴포넌트 재사용하기 - slot 편](https://joshua1988.github.io/web-development/vuejs/slots/) > [Vue.js 공식 문서 -Slot](https://kr.vuejs.org/v2/guide/components-slots.html)
