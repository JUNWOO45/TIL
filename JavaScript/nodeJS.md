Node.js

~~~
nodeJS는 구글 크롬의 V8엔진에 기반해 만들어진 서버 사이드 플랫폼입니다.
Node.js는 코드를 실행할 수 있는 하나의 방법에 불과한 그저 자바스크립트 런타임일 뿐입니다.
~~~

Node.js 특징

~~~
- 비동기 I/O처리, 이벤트 위주
:Node.js 라이브러리의 모든 API는 비동기식입니다.
즉, 데이터를 반환할 때까지 기다리지 않고 다음 API를 실행합니다.
멈추지 않는다고해서 Non-blocking이라고도 하는것 같네요.

- 빠른 속도: 구글 크롬의 V8 자바스크립트 엔진을 사용하여 빠른 속도를 가지고 잇습니다.

- 단일 쓰레드/ 뛰어난 확장성 : 이벤트 루프와 함께 단일 쓰레드 모델을 사용합니다.

- 노 버퍼링: Node.js 어플리케이션엔 데이터 버퍼링이 없고, 데이터를 chunk로 출력합니다.(조각)
~~~



Node.js application 만들기

- 필요한 모듈 import하기
  어플리케이션에 필요한 모듈을 불러올 때에는 require명령을 사용합니다.

  ~~~
  var http = require('http');
  ~~~

- 서버 생성하기

  http인스턴스를 사용하여 http.createServer() 메소드를 실행합니다.

  또한 listen 메소드를 사용하여 3000번 포트와 bind해줍니다.

  ~~~
  http.createServer(function(req, res) {
     res.writeHead(200, {'Content-Type' : 'text/plain'});
     
     response.end("haha node!");
  }).liseten(3000);
  ~~~

- 서버 테스트하기

  ~~~
  var http = require('http');
  
  http.createServer(function(req, res) {
     res.writeHead(200, {'Content-Type' : 'text/plain'});
     
     response.end("haha node!");
  }).liseten(3000);
  ~~~

  ~~~
  $ node main.js
  ~~~

  ~~~
  참고로, 
  res.writeHead(200, {'Content-Type' : 'text/plain'});
  는 지워도 문제없었습니다.
  200을 210으로 수정해보니, status code가 210으로 수정되었습니다.
  
  이 메소드는 반드시 response.end() 전에 실행되어야 한다고 합니다.
  ~~~



NPM

- npm을 사용하여 모듈 설치하기

  ~~~
  npm install <모듈 이름>
  ex) npm install express
  ~~~

- 글로벌 vs 로컬 모듈 설치

  기본적으로 npm은 로컬모드로 모듈을 설치합니다.

- package.json

  package.json은 노드 어플리케이션 / 모듈의 경로에 위치해 있으며 패키지의 속성을 정의합니다.

  프로젝트가 의존하는 모듈과 모듈의 버전정보를 가지고 있습니다.

  

package.json

package.json파일을 작성할 때에는 자바스크립트의 객체 리터럴이 아닌, JSON 포맷이어야 합니다.

- name

  package.json에서 가장 중요한 항목은 "name"과 "version"입니다.

  필수로 입력되어야하는 항목입니다.

- version

  마찬가지로 필수로 입력되어야하는 항목입니다.

- description

  설명을 문자열로 기술합니다.

  npm search로 검색된 리스트에 표시되기 때문에 패키지를 찾아내고 이해하는데에 도움이 되는 항목입니다.

- keywords

  마찬가지로 npm search로 검색된 리스트에 표시되기에 사람들의 이해를 돕습니다.

- dependencies

  의존성을 규정하는 것은 패키지의 이름과 해당 패키지의 버전 범위를 지정한 객체를 통해 이루어진다고 합니다.

  테스트 관련 모듈이나 트랜스파일러 관련 모듈을 dependencies개체에 추가하면 안된다고 합니다.

  운영이 아닌 개발 단계에서만 필요한 의존성 모듈들은 devDependencies에 설치해야합니다.

- devDependencies

  패키지 모듈을 이용하는 사람이라면, 패키지 테스트 및 문서 작성에 사용되는 외부 프레임워크는 아마도 다운로드를 원하지 않을 것입니다.

  이러한 경우에 devDependencies객체에 디펜던시를 추가하는 것이 좋은 방법입니다.

~~~
다시 npm으로 돌아가서...
~~~

- 모듈 제거

  ~~~
  $ npm uninstall express
  ~~~

- 모듈 업데이트

  ~~~
  $npm update express
  ~~~





- 참고 

  node.js : https://velopert.com/241

  package.json : https://programmingsummaries.tistory.com/385

