`SPA(Single Page Application)` 은 모던 웹 패러다임이다.

`SPA`는 `CSR(Client Side Rendering)`을 사용한다.

단일 페이지로 구성되어 네이티브 앱과 유사한 사용자 경험을 제공해준다.

웹 애플리케이션에 필요한 모든 정적 리소스를 `앱 구동 시 최초 한 번 다운로드`한다.

그 후, 필요한 데이터를 받아올 때만 서버와 통신한다.

<br>

하지만 이 세상에 왕도란 없든, 당연히 SPA에도 트레이드오프가 존재한다.

- 초기 구동 속도

  - 정적 리소스를 최초에 한 번 다운로드 하기에, 초기 구동 속도가 비교적 느리다.
  - 하지만 이는 웹팩의 code splitting으로 해결가능하다.

- SEO

  - js파일이 동작하지않으면, 원하는 정보를 표시하지 않는다.
  - 검색엔진 크롤러의 입장에서는 빈 페이지만 보인다.
  - `SSR`로 해결가능하다.

  

그렇다면, `SSR` 이란 무엇일까?

전통적인 웹사이트들은, 서버 연산을 통해서 렌더링하고 완성된 페이지를 응답했다.

이렇나 과정을 `서버 사이드 렌더링`, 즉  `SSR`이라고 한다.

`SSR` 의 장점은 뭐니뭐니해도 SEO이다.

js코드가 동작하기 전에 완성된 형태의 템플릿을 서버로부터 전달받기에, 검색 로봇이 페이지를 크롤링하기에 매우 좋다.

하지만 `SPA` 가 등장했듯, 단점이 존재한다.

- 페이지 이동시 화면 깜빡임
- 페이지 이동시 불필요한 템플릿을 중복하여 로딩
- 서버 렌더링에 따른 성능 하락.
  - 렌더링을 위해 서버 자원을 사용한다는 의미이므로, 불필요한 트래픽이 낭비될 수 있다!

<br>

---

참고로, `SPA` 에서 사용하는 `클라이언트 사이드 렌더링` 은 `HTML5 History API` 를 사용하여 구현한다고 한다.





### Reference

- [https://medium.com/aha-official/%EC%95%84%ED%95%98-%ED%94%84%EB%A1%A0%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EA%B8%B0-1-spa%EC%99%80-ssr%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90-%EA%B7%B8%EB%A6%AC%EA%B3%A0-nuxt-js-cafdc3ac2053](https://medium.com/aha-official/아하-프론트-개발기-1-spa와-ssr의-장단점-그리고-nuxt-js-cafdc3ac2053)
- [https://velog.io/@zansol/%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0-%EC%84%9C%EB%B2%84%EC%82%AC%EC%9D%B4%EB%93%9C%EB%A0%8C%EB%8D%94%EB%A7%81SSR-%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8%EC%82%AC%EC%9D%B4%EB%93%9C%EB%A0%8C%EB%8D%94%EB%A7%81CSR](https://velog.io/@zansol/확인하기-서버사이드렌더링SSR-클라이언트사이드렌더링CSR)
- https://blog.martinwork.co.kr/devops/2019/05/24/server-side-rendering01.html
- https://poiemaweb.com/js-spa