### .nuxt 폴더

-   `.nuxt` 폴더는 동적으로 생성되고, 기본적으로 숨겨져있는 빌드 폴더입니다.

-   `.nuxt` 폴더는 `nuxt dev` 또는 `nuxt build`를 터미널로 실행했을때 자동으로 생성되는 파일들을 가지고 있습니다.

-   `.nuxt` 폴더 내부의 파일들을 수정한다면, 디버깅에는 유용하게 사용할 수 있지만, `dev` 혹은 `build` 커맨드를 실행한다면, 수정했던 파일들이 다시 재생성 됩니다. (수정한 파일들이 무용지물이 됩니다.)

> ⚠ <span style="color:orange">**.nuxt**</span> 폴더는 버전 컨트롤 시스템에 커밋되지 않는 것이 좋습니다. 따라서 <span style="color:orange">**.gitignore**</span>에 반드시 추가 해주세요.

### buildDir 속성

`.nuxt`폴더는 이름이 `.`으로 시작하기 때문에,프로젝트는 `.nuxt` 숨겨진 폴더로 인식합니다. 이를 방지하기 위해 **buildDir** 옵션을 사용할 수 있습니다.

**(e.g) `.nuxt` -> `nuxt-dist`** 로 변경한 경우

**nuxt.config.js**

```javascript
export default {
  ...,
  buildDir: 'nuxt-dist',
  ...,
}
```

**.gitignore**

```javascript
...
nuxt-dist
...
```

> -   [Nuxt js 공식문서](https://nuxtjs.org/docs/2.x/directory-structure/nuxt)
