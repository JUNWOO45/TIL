# HttpClientModule과 HttpClient



사용하는방법

- HttpClientModule 추가
- 컴포넌트에 HttpClient 주입하기
- toPromise() 이용
- 하지만 이렇게 컴포넌트에서 직접 처리하는 방법 말고, 다른 `서비스` 에 주입해서 사용하는 방법을 권장합니다.
  - `서비스` 에 HttpClient 주입
  - 컴포넌트에서 이 `서비스` 를 주입