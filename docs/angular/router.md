# 라우터



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

    