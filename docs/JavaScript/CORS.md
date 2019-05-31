<h1>
    CORS
</h1>

- ~~Ajax에는 Same Origin Policy라는 원칙이 있습니다.~~  

- 비단 Ajax뿐만 아니라, XMLHttpRequest객체는 기본적으로 동일 출처 정책(SOP, Same Origin Policy)의 제약을 받는다고 말하는게 더 정확한듯 합니다.

  - 현재 브라우저에 보여지고 있는 HTML을 내려준 웹서버에게만 Ajax요청을 보낼 수 있습니다.

    - 한 도메인의 Javascript코드를 불러오면 해당 코드 안에서 다른 도메인의 데이터를 요청할 수 없다는 것을 의미하죠.
    - 이를 "<u>크로스 도메인 이슈</u>" 라고 합니다.
    - 동일 출처 정책을 만들때의 웹환경은 지금과 달랐기때문에 보안적 측면에서 이러한 제약은 당연한 것이었습니다. 하지만 최근에는 Ajax가 대중화되었고, OpenAPI가 활성화되면서 클라이언트와 서버가 Ajax로 데이터를 주고받는 형태의 웹 애플리케이션이 일반적이 되었습니다.

  - CORS가 미구현된 웹브라우저에서는 다른 도메인간 통신이 불가능합니다.

  - 우회방법으로 JSONP,  Reverse Proxy, Flash Socket등이 고안되었습니다.

    - JSONP

      JSONP 또는 JSON with padding은 다른 도메인의 데이터를 요청하기 위해 사용하는 자바스크립트 커뮤니케이션 기술입니다.

      이 방식은 script태그가 동일 출처 정책의 제약을 받지 않는 특성을 이용합니다.

      동적으로 생성할 Javascript코드를 script태그를 이용해서 불러옴으로써 동일 출처 정책을 우회하는 것이죠. 

      다음은 저의 이해를 돕기위해 스스로 작성해본 간단한 예시입니다.

      ```
      function success(result) {
          //..
      }
      ```

      1) JSONP방식은 XMLHttpRequest객체를 이용해서 서버로 요청을 전송하는대신 동적으로 script태그를 만들어서 페이지에 삽입합니다.

      그래서 다음과 같이 script태그의 src속성에 호출할 API의 url을 넣고, query string에 callback함수의 이름을 파라미터로 추가합니다.

      ```
      <script src = "http://api.example.com/resources?callback=success"></script>
      ```

      2) 서버는 요청받은 작업을 수행한 후에 클라이언트로 응답을 전송합니다.

      하지만 결과를 그대로 전송하지 않습니다.

      ```
      {key : value}	//이렇게 전송하지 않고,
      ```

      3) 위의 응답결과를 콜백함수의 인자로 전달하여 클라이언트로 전송합니다.

      ```
      success({key : value});
      ```

      4) 결과적으로 Ajax요청의 응답결과를 success콜백 함수가 받아서 실행하는 것입니다.

      JSONP는 동일 출처 정책을 우회하는, 즉 편법이라고 할 수 있습니다.

      JSONP요청은 GET메소드만 이용할 수 있는 단점이 있습니다.


    - Reverse Proxy

      동일 출처 정책(Same Origin Policy)은 <u>"브라우저"</u> 의 보안정책이기 때문에 Backend영역은 이 제약에서 자유롭습니다.

      실제 서버와 클라이언트 사이에 별도의 Proxy서버를 두고, 이 Proxy서버를 이용해서 요청을 주고 받는 방식입니다.

      별도의 서버를 구축해야하고 추가적인 네트워크 요청이 발생한다는것이 단점입니다.

  - 

   

- 그래서 CORS가 뭔데?

  - <h4>CORS는 기술이 아니라, 크로스 도메인 요청에대한 표준입니다.</h4>

    웹브라우저에서 외부 도메인 서버와 통신하기위한 방식을 표준화한 스펙이죠.

  - 크로스 도메인 이슈를 해결하는 표준이 없던 시절에는 JSONP, Reverse Proxy등을 이용해서 우회적으로 동일 출처 정책을 해결했습니다.

    그러다가 2006년 W3C가 크로스 도메인 이슈를 해결하는 표준을 만들기 위한 논의를 시작하여 2013년 12월 CORS공식 권고안이 발표되었습니다!

  - 참고로, Cross Origin Resource Sharing의 약자입니다.

- 왜 CORS가 필요할까?

  - 정상적인 상황이라면 문제되지 않습니다.

    하지만 웹페이지 개발자가 악의적인 목적으로 이를 악용할때 문제가 생깁니다.

    해당 페이지의 자바스크립트 코드 중에 브라우저의 취약점이나 정보를 해커의 사이트로 전송하거나, 광고의 페이지뷰를 의도적으로 높이는 등의 문제가 발생할 수 있기 때문이죠.

    즉, "보안에 취약하다"라는 문제가 있는것입니다.


- CORS의 작동방식

  CORS를 사용하기 위해서는 클라이언트와 서버가 몇가지 추가정보를 주고받아야합니다.

  클라이언트는 CORS요청을 위해 새로운 HTTP헤더를 추가하죠.

  서버는 클라이언트가 전송한 헤더를 확인해서 요청을 허용할지 말지를 결정합니다.

  데이터에 사이드 이펙트를 일으킬 수 있는 HTTP메소드를 사용할 때는 먼저 preflight요청을 서버로 전송해서 서버가 허용하는 메소드 목록을 HTTP OPTIONS헤더로 획득한 다음 실제 요청을 전송합니다.



  - simple request

    기존 데이터에 사이드 이펙트를 일으키지 않는 GET, HEAD, POST요청을 simple request라고 합니다.

    (POST요청의 경우, 서버로 전송하는 Contet-Type이 application/x-www-form-urlencoded, multipart/form-data, text/plain 중에 하나여야 합니다. 이땐 HTTP요청에 커스텀 헤더를 지정하지 않습니다.)

    ```
    var xhr = new XMLHttpRequest();
    var url = "http://example.com/resources/users/";
    
    function simpleRequest() {
        xhr.open("GET", url);
        xhr.onreadystatechange = function() {
            //..
        };
        xhr.send();
    }
    ```


  -  preflight request(사전 요청)

    GET, HEAD, POST이외의 메소드를 이용한 요청의 경우에는 데이터에 사이드 이펙트를만들 수 있기 때문에 브라우저는 preflight요청을 먼저 서버로 전송합니다.

    (POST요청이지만 Content-Type이 application/x-www-form-urlencoded, multipart/form-data, text/plain이 아닌 경우도 여기에 해다합니다. 이때에는 커스텀 헤더를 설정해야합니다.)

    ```
    var xhr = new XMLHttpRequest();
    var url = "http://example.com/resources/users/";
    var body = "<?xml version="1.0"?><user><name>Junwoo</name></user>;
    
    function preflightedRequest() {
        xhr.open("POST", url);
        
        xhr.setRequestHeader("X-Custom-Header", "hello");	//커스텀 헤더 설정
        
        xhr.setRequestHeader("Content-Type", "application/xml");	//Post요청이지만 Content-Type에 의해 preflighted request입니다.
        
        xhr.onreadystatechange = function() {
            //..
        }
        
        xhr.send(body);
    }
    ```



    preflight요청은 실제로 요청하려는 경로와 같은 url에 대해 OPTIONS메서드 요청을 미리 날려보고 요청을 할 수 있는 권한이 있는지 확인합니다.

    - preflight request결과, 허용이 되지않는다면!

      브라우저는 서버가 보낸 Response벙보를 이용하여 허용되지 않은 요청인 경우 405 Method Not Allowed에러를 발생시키고, 실제 페이지의 요청은 서버로 전송하지 않습니다.

    - preflight request결과, 허용된 요청인 경우엔 전송을 합니다!





<h4>
    공부자료
</h4>

- https://www.popit.kr/cors-preflight-%EC%9D%B8%EC%A6%9D-%EC%B2%98%EB%A6%AC-%EA%B4%80%EB%A0%A8-%EC%82%BD%EC%A7%88/
- https://brunch.co.kr/@adrenalinee31/1
- http://wiki.gurubee.net/display/SWDEV/CORS+%28Cross-Origin+Resource+Sharing%29
- https://developer.mozilla.org/ko/docs/Web/HTTP/Access_control_CORS
- http://wit.nts-corp.com/2014/04/22/1400 (정말 좋은 자료.)