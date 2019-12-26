# 타입스크립트 컴파일러



- node.js환경에서 돌아감.

- .ts 파일을 컴파일해서 .js파일을 만들어냄.

  

```typescript
tsc hello.ts
tsc hello.ts --target es6
```



- lib

```
tsc hello.ts --lib es5
```



### 설정파일

- tsconfig.json

```typescript
{
    "include": [
        "src/**/*.ts"
    ],
    "exclude": [
        "node_modules"
    ],
    "compilerOptions": {
        "module": "CommonJS",
        "rootDir": "src",
        "outDir": "dist",
        "target": "ES5"
    }
}

```

```
tsc //라는 명령만 치면,
```

dist폴더에 컴파일됨.

> 이렇게 만들어진 dist 폴더내의 많은 파일들을 webpack같은 번들러로 번들링하게됨.



### 유용한 옵션

- sourceMap
- removeComments
- noImplicitAny