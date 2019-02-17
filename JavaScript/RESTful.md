<h1>
    REST
</h1>



- REST는 representational state transfer의 약자입니다.

  우리말로 바꿔보면 '대표적인 상태 전달' 정도가 될 것입니다.

  ```
  "자원(resource)의 대표(representation)에 의한 상태 전달"
  
  - 자원이란, 소프트웨어가 관리하는 모든 것이 될 수 있습니다.
  문서, 그림, 데이터, 혹은 소프트웨어 그 자체를 의미할 수 있습니다.
  "자원의 대표"란 자원을 대표하기위한 이름을 의미합니다.
  예를들어, DB에 노래들이 저장되어있다면, 이 노래들에 관한 정보가 자원(resource)입니다.
  "자원의 대표"는 musics가 됩니다.
  
  - 상태전달이란, 데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달하는 것을 의미합니다.
  ```

- REST의 구성요소

  - 리소스: 접근할 대상(URI)
  - 메소드: 리소스에 대한 행위(HTTP Method)
  - 메시지: HTTP 헤더, HTTP 바디, 응답 상태코드

  ```
  즉, REST는 어떤 자원(리소스)에 어떤 행위(메소드)를 어떻게(메시지)할 것인지를 HTTP 기반으로 정해놓은 아키텍쳐라고 할 수 있습니다.
  ```

  

- 리소스

  ```
  https://api.domain.com/musics
  노래정보 콜렉션
  
  https://api.domain.com/musics/1
  1번 노래 정보
  
  https://api.domain.com/musics/1/image
  1번 노래 커버이미지
  ```

- 메소드

  ```
  REST에서는 표준 HTTP Method를 통해 리소스에대한 행위를 정의합니다.
  
  POST: Create
  GET: Read
  PUT: Update
  DELETE: Delete
  ```

- 메시지

  ```
  REST에서 자원에대한 정보는 HTTP바디, HTTP 헤더, 응답상태코드를 활용합니다.
  ```

  

- 예시

  1.

  ```
  1번 member를 지우려고 할 때
  
  GET /members/delete/1
  ```

  위 예시는 REST가 제대로 적용되지않은 URI입니다.

  URI는 "자원"을 표현하는데에 중점을 두어야합니다.

  delete는 "행위에 대한 표현"입니다.

  아래와 같이 수정할 수 있습니다.

  ```
  DELETE /members/1
  ```

  2.

  ```
  member를 추가하려고 할 때
  
  GET /members/show/2
  ```

  위 예시도 REST가 제대로 적용되지않은 URI입니다.

  GET은 리소스 생성이 아니라 리소스를 읽는 메소드입니다.

  수정을 하려면 POST 메소드를 사용해야합니다.

  ```
  POST /members/2
  ```

  

- URI 설계 시 주의할 점

  1. 슬래시 구분자( / )는 계층 관계를 나타내는 데 사용합니다.

     ~~~
     https://vanillacoding.com/houses/apartments
     https://vanillacoding.com/animals/cat
     ~~~

  2. URI 마지막 문자로 슬래시( / )를 포함하지 않습니다.

  3. 하이픈( - )은 URI 가독성을 높이는데에 사용합니다.

     불가피하게 긴 URI경로를 사용하게 되면 하이픈을 사용해서 가독성을 높일 수 있습니다.

  4. 밑줄( _ )은 URI에 사용하지 않습니다.

     밑줄은 보기어렵거나 문자가 가려지기도 하기에 밑줄대신 하이픈을 사용하는 것이 좋습니다.

  5. URI경로에는 소문자를 사용합니다.

  6. 파일 확장자는 URI에 포함시키지 않습니다.

     ex) .json, .xml, .jpg...



- 리소스 간의 관계를 표현하는 방법

  REST 리소스 간에는 연관관계가 있을 수 있습니다.

  ~~~
  /리소스명/리소스 ID/관계가있는 다른 리소스명
  ex) GET /users/{userid}/devices
  (users에 포함되어있는 userid가 devices를 가지고 있을 때)
  
  ex) GET /users/{userid}/likes/devices
  (사용자가 "좋아하는"디바이스 목록만을 표현하는 경우)
  ~~~

  

- 자원을 표현하는 Collection과 Document

  Document는 단순한 문서, 객체로 이해해도 됩니다.

  Collection은 이러한 Document들의 집합입니다.

  ~~~
  https://example.com/sports/soccer
  ~~~

  위 URI에서는 sports라는 컬렉션과 soccer라는 도큐먼트가 있는 것입니다.

  ~~~
  https://example.com/sports/soccer/players/13
  ~~~

  위 URI에서는 sports, players라는 컬렉션과, soccer,13(13번 선수)를 의미하는 도큐먼트가 URI를 구성하고 있습니다.