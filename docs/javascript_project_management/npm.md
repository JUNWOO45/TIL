# npm 



처음 공부할때, 저는 npm을 잘 이해하지못했습니다.

물론 지금도 완벽히 파악하고있지 못합니다.

지금의 저에게 npm은, 어릴때 장난감을 넣던 **장난감상자** 의 의미입니다.

npm에서는 재사용가능한 코드들을 module, package라고 부릅니다.

package.json에는 이러한 module, package에대한 파일 정보가 들어있습니다.



## 명령어

###package.json 생성

- node module들을 관리하기위해 package.json을 설정해주어야 하는데요.

  ```
  $ npm init
  ```

  명령어를 사용해서 생성합니다.

  ```
  $ npm init -y
  ```

  으로 default정보로 package.json을 생성할 수 있습니다.

  

###패키지 설치 & 업데이트

- node module을 설치하거나 package.json을 업데이트 해줄때 사용합니다.

  ```
  $ npm install 패키지명
  $ npm i 패키지명
  ```

  > npm 5버전 이후에는, 기존에 사용하던 --save옵션이 default가 되었습니다.
  >
  > 이제 --save 옵션은 사용하지 않아도 된다고 하네요!


  이렇게 패키지를 설치하면, node_modules 파일 밑에 패키지가 설치됩니다.

  이렇게 설치된 패키지는 `local` 에 설치된 건데요.



###Global vs Local

- Global로 설치하면, node_modules에 추가되는 것이 아니라 시스템레벨에 설치됩니다.

  그래서, 다음과 같이 webpack을 설치하면..

  ```
  $ npm install webpack webpack-cli -g
  ```

  터미널에서 명령어를 사용할 수 있게되는거죠.

  ```
  $ webpack
  ```

- 반면에 Local로 설치를 하게 되면, 명령어를 실행할 수 있게 되는것이 아니라 node_modules밑에 패키지가 생성됩니다.

  require( )로 땡겨올(?) 수 있게 되는거죠.

  

###install **--save** & install **--save-dev**

- **--save** 는 앱을 구동시킬 때 필요한 모듈 & 라이브러리를 설치할 때 사용합니다.

  ex) vue, jquery

  ```
  //package.json
  
  "dependencies": {
  	"jquery": "^3.4.1",
  	"vue": "^2.3.3"
  }
  ```

  

- **--save-dev** 는 **개발**시 에 필요한 모듈 & 라이브러리를 설치할 때 사용합니다.

  ex)  nodemon, test&build tool

  ```
  //package.json
  
  "devDependencies": {
  	"gulp": "^3.9.6"
  }
  ```

  



