# Webpack

웹팩이란?

- 서로 연관 관계가 있는 웹 자원들을 js, css, img와 같은 static한 자원으로 변환시켜주는 모듈 번들러

  

웹팩 철학

1. 모든 웹 자원(html, css ,js)을 모듈형태로 로딩 가능

   ```
   require('base.css');
   require('main.js');
   ```

2. 초기에 모두 로딩하지 않고, 필요할 때 필요한 것만 로딩하여 사용



진행을 하면서,

```
$ webpack app/index.js --output dist/bundle.js --mode development
```

app/index.js는 번들링할 대상이고, dist/bundle.js는 결과물.



