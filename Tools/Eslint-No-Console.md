# Eslint no-console

### console.log

웹 개발시 디버깅 목적으로 브라우저의 console.log 메서드를 자주 사용하게 됩니다. 사용하기 간편하고, 애플리케이션의 동작에 직접적인 영향을 주지 않기 때문에 개발자 도구의 Debugger 보다 더 자주 사용합니다.

```javascript
if (condition) {
    //...
} else {
    console.log("이 메시지가 출력되면 절대 안된다!");
    console.log("뭔가 잘못 되었다.");
}
```

console.log 는 가장 간편한 디버깅 메소드이긴 하지만 운영에 배포되는 어플리케이션에는 포함되지 않는 것이 좋습니다. 불필요한 코드 이기도 하고 보안 이슈가 발생할 가능성도 있습니다. 무엇보다 **개발자가 신경을 안 썼다는 티**가 나서 좋지 않습니다.

[no-console - Rules](https://eslint.org/docs/rules/no-console)

### no-console 에러

1. Eslint 인라인 설정 - 파일 전체

```javascript
/* 파일 전체에 no-console 룰 사용 안함, 파일 최상단에 선언 */
/* eslint-disable no-console */
console.log("hello");
```

2. Eslint 인라인 설정 - 1 라인

```javascript
/* 라인 단위로 no-console 룰 적용 제외 */
/* eslint-disable-next-line no-console */
console.log("world");
```

3. eslintrc.js rules 변경

```javascript
module.exports = {
    rules: {
        "no-console": "off",
    },
};
```

## 참조

[운영 빌드 시 console.log 제거하기. 덤으로 no-console 에러도 해결](https://gitabout.com/3)
