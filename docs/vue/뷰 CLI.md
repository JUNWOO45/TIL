<h1>
  Vue CLI
</h1>



우선, cli가 설치되어있지않다면 설치해줍니다.

```
$ npm install -global vue-cli
```

그 다음 단계는, 2가지로 나뉠 수 있습니다.

webpack과 webpack-simple

webpack에 익숙하지않은 저같은 경우에는 webpack-simple이 더 좋을듯합니다.

```
$ vue init webpack-simple
```



현재 디렉토리에 프로젝트 생성할거냐..프로젝트이름이 뭐냐.. 여러가지 질문을 하네요.

설정을 해줍니다!



설치가 완료되면, 이제 npm install을 해줘야합니다.

그런데, 왜 npm install을 하는걸까요?

vue init webpack-simple로 설치한 프로젝트의 package.json을 가보시면,

devDependencies와 dependencies들을 볼 수 있습니다.

이 라이브러리들을 다운받기 위해서 npm install을 해주는것입니다.

```
$ npm install
```

을 실행시켜주면, package.json의 의존성이있는 라이브러리들을 node_modules라는 폴더 아래에 설치하게됩니다.

```
$ npm run dev
```

를 하면, webpack의 dev server로 접속!



이 방법과 마찬가지로, 

```
$ vue init webpack
```

으로 설치를 하게되면,

물어보는 질문도 훨씬 많아지고, 생성된 프로젝트구조도 훨씬 복잡합니다.

경험과 공부가 필요할 듯 합니당.

