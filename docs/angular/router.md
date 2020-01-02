# 라우터



## 기본

- RouterModule import.

  - import { RouterModule, Route  } from '@angular/router';

- 사용하고자 하는 모듈에 import.

  - RouterModule.forRoot(<Route 배열>)

  - ```
    const routes: Routes = [
      { path: '', component: HomeComponent },
      { path: 'login', component: LoginComponent }
    ];
    
    @NgModule({
      imports: [RouterModule.forRoot(routes)],
      exports: [RouterModule]
    })
    ```

- 템플릿에 커스텀 라우터 엘리먼트 추가

  - ```html
    <router-outlet></router-outlet>
    ```

<br>

## a 태그를 사용

- a태그의 attribute directive를 사용한다. (routerLink) 

```
<a routerLink="/"> 홈 </a>
```



- routerLinkActive

  - url이 일치하면, class를 부여

  - ```
    <a routerLink="signup" routerLinkActive="highlight">
    ```

    