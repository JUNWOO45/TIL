# Webpack

##웹팩이란?

- 서로 연관 관계가 있는 웹 자원들을 js, css, img와 같은 static한 자원으로 변환시켜주는 모듈 번들러

  

##웹팩 철학

1. 모든 웹 자원(html, css ,js)을 모듈형태로 로딩 가능

   ```
   require('base.css');
   require('main.js');
   ```

2. 초기에 모두 로딩하지 않고, 필요할 때 필요한 것만 로딩하여 사용



##Webpack 기본

### Entry

- 시작점을 설정합니다.
- 복수의 엔트리 포인트를 설정할 수 있습니다.

### Output

- entry에서 설정하고 묶은 파일의 결과값을 설정합니다.

### Loader

- 기본적으로 웹팩은 자바스크립트 파일만 처리가 가능합니다.

- 로더를 이용해서 다른 형태의 웹자원들(img, css, typescript, html 등)을 js로 변환하여 로딩하게 됩니다.

  ```
  module.exports = {
  	entry: {},
  	output: {},
  	module: {
  		rules: [
  			{
  				test: /\.css$/,
  				use: ['style-loader', 'css-loader']
  			}
  		]
  	}
  }
  ```

  module부분을 로더라고 보면 됩니다.

- 모듈은 배열의 오른쪽에서 왼쪽으로 로딩됩니다.

  - 위 코드 같은 경우에는 css-loader가 먼저 로딩되고, style-loader가 로딩됩니다.

### Plugins?

- 파일별 커스텀 기능을 사용할 수 있게 해줍니다.

  ```
  module.exports = {
  	entry: {},
  	output: {},
  	module: {},
  	plugins: [
  		new webpack.optimize.UglifyJsPlugin()
  	]
  }
  ```

- 일반적으로 사용하는 css-loader 나 style-loader같은 로더와 플러그인은 뭐가 다르길래 module과 plugins로 나뉜걸까요?

  - 대략 번들링하는 과정에 사용되는 것이 로더... 번들링이 끝난 뒤 결과값에 추가작업을 해주는게 플러그인같네요



### Resolve옵션

```
module.exports = {
	mode: 'development',
	entry: './app/index.js',
	output: {
		filename: 'bundle.js',
		path: path.resolve(__dirname, 'dist')
	},
	resolve: {
		alias: {
			Vendor: path.resolve(__dirname, './app/vendor/')
		}
	}
}
```

> resolve옵션은 path.resolve()와 다른것!
>
> 헷갈리지 말자.

- config파일에 resolve를 추가해서 사용할 수 있습니다.

- alias

  - 특정 모듈을 로딩할 때 alias 옵션을 사용해서 로딩할 수 있습니다.

    ```
    alias: {
    	Utilities: path.resolve(__dirname, 'family/father/information/')
    }
    ```

    ```
    // import Utility from '../../family/father/information/name'
    // 위는 아래와 같습니당
    
    import Utility from 'Utilities/name'
    ```

- modules

  - require() 나 import 등 모듈을 로딩할 때 어느 폴더를 기준으로 할 지 정하는 옵션입니다.

    ```
    modules: ["node_modules"]	//default
    modules: [path.resolve(__dirname, "family/father"), "information"]
    // family/father/information
    ```

    

---

## webpack 빌드를 위한 개발 서버 구성

- webpack-dev-server : webpack 자체에서 제공하는 개발 서버입니다.
- webpack-dev-middleware: 서버가 이미 구성된 경우, webpack을 미들웨어로 구성해서 서버와 연결시켜줍니다.



### webpack dev server

- page reload해주는 webpack 개발용 node.js 서버입니다.



### 설치 및 실행

- 우선 설치합니다

```
$ npm install webpack-dev-server --save-dev
```

- 설치 후 다음 명령어로 서버를 실행합니다.

```
$ webpack-dev-server --open
```

- 또는 package.json에 명령어를 등록해서 실행가능!

```
"scripts": {
	"start": "webpack-dev-server"
}
```



### Options

- publicPath: Webpack으로 번들할 파일들이 위치하는 곳입니다.

  - default값은 '/'입니다.

  - **중요한 점은, 항상 '/'를 앞, 뒤에 붙여야 합니다!!**

  ```
  module.exports = {
  	//...
  	devServer: {
  		publicPath: "/assets/"
  	}
  }
  ```

- contentBase: 서버가 로딩할 static 파일 경로를 지정합니다.

  - default값은 working directory입니다.

    ```
    module.exports = {
    	//...
    	devServer: {
    		//공식문서에서 절대경로를 사용하는 것을 추천한다고 하네요!
    		contentBase: path.join(__dirname, "public")
    	}
    }
    ```

    ```
    module.exports = {
    	//...
    	devServer: {
    		contentBase: [path.join(__dirname, "public"), path.join(__dirname, "assets")]
    	}
    }
    ```

    ```
    module.exports = {
    	//...
    	devServer: {
    		//비활성화
    		contentBase: false
    	}
    }
    ```

- compress: gzip압축방식을 사용해서 웹자원의 사이즈를 줄일 수 있습니다.

  ```
  module.exports = {
    //...
    devServer: {
      contentBase: path.join(__dirname, 'dist'),
      compress: true,
      port: 9000
    }
  };
  ```

  

### webpack-dev-server를 테스트해봤을때,

```
$ webpack-dev-server 
```

또는

```
$ npm start //package.json의 script에 'webpack-dev-server'를 등록했다고 가정
```

을 했을 때,

물리적으로 dist폴더가 생기지 않았습니다.

정확하지는 않지만, in memory에 저장? 되는 식이라고 하네요.

따라서 나중에 배포를 할 때는

```
$ webpack
```

을 실행해서 물리적으로(?) dist 폴더를 만들어줘야합니다.



---

## Webpack 명령어

- webpack : 웹팩 빌드 기본 명령어

- webpack -p : minification기능이 들어간 빌드(주로 배포용으로 사용)

- webpack -w(--watch) : 빌드할 파일의 변화를 감지

- webpack -d : sourcemap을 포함하여 빌드

- webpack --display-error-details: error발생시 디버깅정보 상세출력

- webpack --optimize-minimize --define process.env.NODE_ENV="'production'": 배포용

  

### webpack -w

webpack설정에 해당하는 파일변경 발생시 자동으로 번들링을 다시 진행시키는 명령어입니다.

```
$ webpack -w
또는
$ webpack --watch
```

기존에 `$ webpack` 명령어만 실행했을때에는, 또 번들링을 진행하려면 `$webpack`명령어를 다시 입력해주어야했는데, -w옵션을 지정해주니깐 그러지않아도 되네여.

