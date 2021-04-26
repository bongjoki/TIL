### 교차 출처 리소스 공유 (CORS)란?

**교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)**는 추가 HTTP 헤더를 사용하여, **한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제입**니다. 웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행합니다.

(e.g) 교차 출처 요청의 예: https://domain-a.com 의 프론트 엔드 JavaScript 코드가 XMLHttpRequest를 사용하여 https://domain-b.com/data.json 을 요청하는 경우.

![](https://mdn.mozillademos.org/files/14295/CORS_principle.png)

### 해결 방법

프론트의 경우 **Request Header에 CORS 관련 옵션을 넣어주는 것**이고
서버의 경우에는 **Response Header에 해당하는 프론트의 요청을 허용**한다는 내용을 넣어주면 된다

### 참조

> -   [교차 출처 리소스 공유 (CORS)
>     ](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)
> -   [CORS 교차 출처 리소스 공유](https://velog.io/@dorazi/CORS)
