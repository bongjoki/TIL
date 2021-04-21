### node-sass , sass-loader, @nuxtjs/style-resources

yarn 이용하여 node-sass, sass-loader, @nuxtjs/style-resources 를 설치합니다.
sass-loader 설치(11.0.0)후 오류가 나서 버전을 다운그레이드 하여 다시 설치하였습니다. 설치한 버전입니다.

[TypeError: this.getOptions is not a function [closed]](https://stackoverflow.com/questions/66082397/typeerror-this-getoptions-is-not-a-function)

**package install**

```shell
yarn add --dev @nuxtjs/style-resources sass-loader@10 node-sass@5
```

**package.json**

```javascript
{
...
"sass-loader": "^10",
"node-sass": "^5.0.0"
...
}
```

**nuxt.config.js**

```javascript
modules: [
...
'@nuxtjs/style-resources',
...
],
전역 스타일 scss 설정
css: ['~assets/scss/index.scss'],
변수, 믹스인 scss 설정
styleResources: {
scss: ['~/assets/scss/variables.scss', '~/assets/scss/query.scss'],
},
```

### 참조

> [nuxt.js 에서 sass/scss 사용하는 방법](https://markettraders.kr/nuxt-js-scss-import/)
