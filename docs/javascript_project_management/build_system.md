<h1>BuildSystem</h1>


BuildSystem이란 것은, 컴파일을 사용하는 언어에서 채택하는 방식입니다.

ex) C, C++, JAVA...

자바스크립트같은 인터프리터 언어는 빌드가 필요하지않아서 BuildSystem대신에 package manager라는걸 사용한다고 합니다.

ex) js의 npm, bower, yarn 등등...



자바스크립트에서도 BuildSystem을 사용하기에....제가 이런 공부를 하고 있겠져

즉, 자바스크립트도 컴파일을 한다..!



예를 들어, 타입스크립트나 커피스크립트를 사용하고있다면 자바스크립트로 번역해주어야합니다.

만약 바닐라 자바스크립트를 쓰고 있다면..? 이것도 버전별로 컴파일해줘야합니다.

html에 pug나 ejs를 쓸 경우,

css에 sass나 scss를 쓸 경우,

vue나 react를 쓸 경우 모두 "컴파일"을 해주어야합니다.



이러한 자바스크립트 BuildSystem의 대표적인 예는 gulp라고 합니다.

몇번 들어본 친구네요.

gulp는 정말 순수한 build system이라고 합니다.

대표적인 컴파일 언어인 JAVA의 buildSystem인 maven이나 gradle의 경우 buildSystem + package manager라고 합니다.

하지만 gulp는 패키지매니저가 될 수 없다고 해요.

그래서 항상 npm이나 yarn같은 패키지매니저와 같이 사용해야한다고 합니다.



사실 요즘 대세는 Webpack이라고 합니다.

모듈 번들러를 공부하면서 배운 Webpack이네요.

Webpack을 더 잘 이해하기위해서는 Webpack이전에 많이 쓰였던 gulp와 grunt에대한 이해가 필요합니다.

<h2>
  Grunt와 Gulp
</h2>

grunt와 gulp는 사람의 실수나 반복적인 작업을 줄여주기위한 자동화 툴(task runner)입니다.

CSS와 JS파일을 concat, minify, compress, uglify를 하는데 많이 사용된다고 합니다.

즉, 사전에 필요한 반복적인 작업들을 간단한 작업만으로 진행할 수 있도록 도와준다고핣니다.

<h2>
  Webpack
</h2>

핵심부터 얘기하면, Webpack은 이들을 1:1로 대체한다기보다는, 이 기능들이 포함되어있고 더 많은 작업 또한 할 수 있어서 Webpack을 씁니다.

Webpack은 Browserify와 같은 "의존성 관리 기능"까지 포함하고 있습니다.

정리해보면, Grunt, Gulp는 오직 리소스들에대한 툴로써 사용되며, 의존성 관리기능이 없습니다.

Browserify는 비슷한 도구이지만, 속도면에서 Webpack이 더 우월합니다!

```
Webpack = (Grunt || Gulp) + Browserify
```

라고 할 수 있습니다.

