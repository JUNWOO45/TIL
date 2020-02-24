# Angular Universal

일반적인 Angular 애플리케이션은 브라우저에서 실행된다.

하지만 Angular Universal을 사용하여 서버에 미리 생성해둔 애플리케이션을 클라이언트가 실행하고, 그 이후에 앱을 다시 부트스트랩하는 테크닉이 가능하다.

- SEO
- 모바일, 저사양 장비에서의 성능을 끌어올리기위해
- 첫 렌더링 페이지를 빠르게 표시하기위해

자세한건 [여기](https://angular.kr/guide/universal) 에서 확인.

<br>

---

테스트해봤는데 어렵지않다.

### 1. 우선 모듈을 설치해주자.

```typescript
ng add @nguniversal/express-engine --clientProject 프로젝트이름
```

Angular Universal을 위한 몇가지 설정파일들이 설치된다.

### 2. `universal-interceptor.ts` 파일을 생성해주자.

```typescript
import {Injectable, Inject, Optional} from '@angular/core';
import {HttpInterceptor, HttpHandler, HttpRequest, HttpHeaders} from '@angular/common/http';
import {Request} from 'express';
import {REQUEST} from '@nguniversal/express-engine/tokens';

@Injectable()
export class UniversalInterceptor implements HttpInterceptor {

  constructor(@Optional() @Inject(REQUEST) protected request: Request) {}


  intercept(req: HttpRequest, next: HttpHandler) {
    let serverReq: HttpRequest = req;
    if (this.request) {
      let newUrl = `${this.request.protocol}://${this.request.get('host')}`;
      if (!req.url.startsWith('/')) {
        newUrl += '/';
      }
      newUrl += req.url;
      serverReq = req.clone({url: newUrl});
    }
    return next.handle(serverReq);
  }
}

```



### 3. app.server.module.ts에 추가해주자.

```typescript
import {HTTP_INTERCEPTORS} from '@angular/common/http';
import {UniversalInterceptor} from './universal-interceptor';

@NgModule({
  ...
  providers: [{
    provide: HTTP_INTERCEPTORS,
    useClass: UniversalInterceptor,
    multi: true
  }],
})
export class AppServerModule {}
```



끝이다.

`package.json` 에서 명령어들을 확인할 수 있다.

실행하기 위해서는 우선 빌드해야한다.

```
npm run build:ssr
```

```
npm run serve:ssr
```

