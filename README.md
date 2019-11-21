# spring-security-gradle

## Maven, Gradle을 사용한 Angular 빌드
  - npm 빌드를 사용하여 Angular 빌드후 서버단의 resource폴더에 입력하는 방식
  - Maven, Gradle의 resource 폴더가 조금씩 다르니 확인 필요
  - Gradle의 경우 VS Code 사용불가.

## Angular와 Spring Security를 사용한 예제
  - 인증을 받지 않을 경우 브라우저 팝업이 뜨게 되어 있는데 이를 수정
    - 헤더에 WWW-Authenticate 값이 들어 있을 경우 브라우저에서 강제 인증 팝업 노출
    - XHR(XMLHttpRequest) = ajax 호출
    - 클라이언트에서 "X-Requested-With=XMLHttpRequest"값을 헤더값에 추가하여 서버 호출.(X의 경우 표준이 아님 나타냄. 즉 커스텀 헤더값)
    - ajax 호출임을 서버에 알리기 위한 부분.
    - CORS 통신일 경우 origin 파라메터 덕분에 ajax 임을 확인할 수 있음.
    - HTML5 일경우에도 origin 파라메터가 추가되기 때문에 ajax 임을 확인할 수 있음.
  - logout 호출시 (403 forbidden)에러나는 부분 수정
    - logout은 Spring Security에 기본 포함된 API
    - 기본적으로 CSRF(Cross-Site Request Forgery) 적용해야 호출 가능함
  - 쿠키 옵션
    - http only
      - 브라우저에서 쿠키에 접근할 수 없음
      - CSRF cookies 사용시 해당 옵션을 꺼야함
    - secure cookies
      - https가 아닌 통신에서 쿠키를 전달하지 않음
  - 세션 고정 공격
    - 사용자가 사용하는 세션이 아닌 특수한 사용자가 사용하는 세션을 통한 해킹
    - session id를 호출마다 변경시키는 방법으로 해결 가능
