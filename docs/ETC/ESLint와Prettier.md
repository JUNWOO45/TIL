# ESLint와 Prettier

<br>

## ESLint

### Install

```
$ npm i eslint --save-dev
// or 

$ yarn add eslint --dev
```

### setup configuration file

```
$ npx eslint --init
```

### run

```
$ npx eslint yourfile.js
```

공식 문서에서는 eslint를 글로벌로 설치하는 것을 추천하진 않는다. 그냥 개별 프로젝트마다 설정하길 추천함.

### check configuration file

`eslint --init` 명령어를 실행 후, 설정을 고르면 `.eslintrc.js` 파일이 생성된다.

```
module.exports = {
    "env": {
        "browser": true,
        "commonjs": true,
        "es2020": true
    },
    "extends": "eslint:recommended",
    "parserOptions": {
        "ecmaVersion": 11
    },
    "rules": {
    }
};

```

<br>

ESLint는 주로 prettier와 함께 사용한다.

## Prettier 

### Install

```
$ npm install prettier --save-dev --save-exact
```

<br>

### 추가 모듈들

ESLint와 Prettier를 함께 사용하기 위해서는 추가로 모듈들을 설치해야합니다.

- eslint-config-prettier
  - eslint와 prettier의 충돌 설정들을 비활성화합니다.
- eslint-plugin-prettier
  - 코드 포매팅을 할 때 prettier를 사용하게하는 규칙을 추가합니다.

### 추가 모듈 설치

```
$ npm install eslint-plugin-prettier eslint-config-prettier --save-dev
```

<br>

### .eslintrc.js에 내용 추가

```
{
	...
	
  "plugins": ["prettier"],
  "extends": ["eslint:recommended", "plugin:prettier/recommended"],
  "rules": {
    "prettier/prettier": "error"
  },
  
  ...
}

```

<br>

### vscode extension

vscode에서 eslint와 prettier를 사용하기위해 extension을 설치합니다.



### vscode 설정

`cmd` + `,` 를 누르면 vscode 설정으로 들어갈 수 있다.

![configuration 1](/Users/ns/Documents/works/fe-study/parkjunwoo/pic/configuration1.png)

그리고 저 빨간 박스를 누르면 설정파일을 JSON으로 확인할 수 있다.

몇가지 설정들이 이미 저장되어있는데, 다음 설정들을 추가해줍니다.

```javascript
{
    // 기본 formatOnSave는 꺼두고
    "editor.formatOnSave": false,
    // 자바스크립트는 켜둔다.
    "[javascript]": {
        "editor.formatOnSave": true
    },
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
```



<br>

### Prettier 설정

`.prettier.js` 파일을 만들고 [옵션](https://prettier.io/docs/en/options.html)을 설정해줍니다.

```
{
    "trailingComma": "es5",
    "tabWidth": 2,
    "semi": true,
    "singleQuote": true
}
```

<br>

이렇게 환경설정을 구성하고 사용해봤습니다.

개인적으로 저는 jest를 사용하고 있던 tdd프로젝트에서 환경설정을해서 jest 옵션을 추가했습니다.

환경설정은 [eslint-plugin-jest](https://www.npmjs.com/package/eslint-plugin-jest) 의 Usage를 보고 설정했습니다.

### 모듈 설치

```
$ npm i eslint-plugin-jest --save-dev
```

### 린트 설정 추가

```javascript
//.eslintrc.js

module.exports = {
  plugins: ["prettier", "jest"],
  
  ...
  ,
  extends: [
    "eslint:recommended",
    "plugin:prettier/recommended",
    "plugin:jest/recommended",
  ],
  
  ...
  
  rules: {
    "prettier/prettier": "error",
    "jest/no-disabled-tests": "warn",
    "jest/no-focused-tests": "error",
    "jest/no-identical-title": "error",
    "jest/prefer-to-have-length": "warn",
    "jest/valid-expect": "error",
  },
};

```



---

## Reference

[https://feynubrick.github.io/2019/05/20/eslint-prettier.html](https://feynubrick.github.io/2019/05/20/eslint-prettier.html)

