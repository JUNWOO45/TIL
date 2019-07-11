# Webpack

###웹팩이란?

- 서로 연관 관계가 있는 웹 자원들을 js, css, img와 같은 static한 자원으로 변환시켜주는 모듈 번들러

  

###웹팩 철학

1. 모든 웹 자원(html, css ,js)을 모듈형태로 로딩 가능

   ```
   require('base.css');
   require('main.js');
   ```

2. 초기에 모두 로딩하지 않고, 필요할 때 필요한 것만 로딩하여 사용



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

    