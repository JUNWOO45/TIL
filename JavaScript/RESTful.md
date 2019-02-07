RESTful이란?

~~~
REST는 Representational State Transfer라는 용어의 약자로, 웹의 장점을 최대한 활용할 수 있는 아키텍쳐를 뜻합니다.

REST API는 다음의 구성으로 이루어져있습니다.
- 자원(Resource) - URI
- 행위(Verb) - HTTP METHOD
- 표현(Represetations)

REST의 특징
1.Uniform(유니폼 인터페이스)
Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 의미합니다.

2.Stateless(무상태성)
작업을 위한 상태정보를 따로 저장하고 관리하지 않습니다.

3.Cacheable(캐시가능)
REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용가능하다는 점입니다.
따라서 HTTP가 가진 캐싱 기능을 적용할 수 있습니다.

4.Self-descriptiveness(자체 표현 구조)
REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해할 수 있는 자체 표현 구조로 되어 있다는 점입니다.

5.Client - Server 구조
REST서버는 API제공, 클라이언트는 사용자 인증이나 컨텍스트등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기때문에 클라이언트와 서버에서 개발해야 할 내용이 명확하고 서로간의 의존성이 줄어듭니다.

6.계층형 구조
REST서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.

REST API 디자인 가이드
- REST API설계 시 가장 중요한 항목은 다음 2가지라고 할 수 있습니다.
1) URI는 정보의 자원을 표현해야 합니다.
2) 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현합니다.

1)URI는 정보의 자원을 표현해야한다.(리소스명은 동사보다는 명사를 사용)
GET /members/delete/1
이건 REST를 제대로 적용하지 않은 URI입니다.
URI는 자원을 표현하는데 중점을 두어야 합니다.
delete같은 행위에 대한 표현이 들어가서는 안됩니다.
2)자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE등)로 표현해야합니다.
위의 잘못된 URI를 HTTP Method를 통해 수정해본다면,
DELETE /members/1
로 수정할 수 있습니다.
회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할때는 POST Method를 사용합니다.

회원정보를 가져오는 URI
GET /members/show/1 (x)
GET /members/1

회원을 추가할 때
GET /members/insert/2 (x) - GET메서드는 리소스 생성에 맞지 않습니다.
POST /members/2 (o)

~~~



