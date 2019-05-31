<h1>
  vue cli 설치할 때 생긴 문제
</h1>



```
internal/modules/cjs/loader.js:584
    throw err;
    ^

Error: Cannot find module '../lib/utils/unsupported.js'
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:582:15)
    at Function.Module._load (internal/modules/cjs/loader.js:508:25)
    at Module.require (internal/modules/cjs/loader.js:637:17)
    at require (internal/modules/cjs/helpers.js:22:18)
    at /usr/local/lib/node_modules/npm/bin/npm-cli.js:19:21
    at Object.<anonymous> (/usr/local/lib/node_modules/npm/bin/npm-cli.js:152:3)
    at Module._compile (internal/modules/cjs/loader.js:701:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:712:10)
    at Module.load (internal/modules/cjs/loader.js:600:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:539:12)
```

라는 문제가 발생..

당연히 구글링 시작.

<https://stackoverflow.com/questions/44363066/error-cannot-find-module-lib-utils-unsupported-js-while-using-ionic>

처음엔

```
$ brew update
```

```
$ brew uninstall node
```

```
$ brew uninstall --force node 
이건 터미널에서 추천해줘서 추가로 진행..
```

```
$ brew install node
```

```
$ brew link --overwrite node
이 커맨드는 무슨 의미인지 모르고 진행...
```



했지만 효과가 없었습니다.



<h3>
  해결법
</h3>



```
$sudo rm -rf /usr/local/lib/node_modules/npm
$brew reinstall node
```



을 진행하니..바로해결..!

