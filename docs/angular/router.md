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

    ```
    <a routerLink="signup" routerLinkActive="highlight">
    ```

  

- routerLinkActiveOptions

  - "/" 같은 경우, 다른 주소에서도 동작해버리니깐, 주소가 똑같을때에만 동작하도록..
  - ex) === 같은 느낌.

  ```html
  <a routerLink="/" routerLinkActive="green" [routerLinkActiveOptions]="{exact: true}">홈</a>
  ```



## a 태그 사용하지않고 라우팅 이용하기

- 사용하려는 컴포넌트에서 Router 서비스 주입
- 주입된 서비스의 navagate 함수 호출하기

```typescript
id;

constructor(private route: ActivateRoute, private router: Router) {}

ngOnInit() {
  this.url = this.route.snapshot.queryParamMap.get('id');
}

click() {
  setTimeout(() => {
    this.router.navigate([this.id || '']);
  })
}
```





## 동적라우팅

### - 라우터에서 parameter 사용하기

- Routes에 `:id` 처럼 설정
- 사용하는 컴포넌트에서 ActivatedRoute 서비스 주입
- 주입된 서비스를 이용해서 `:id` 가져오기
  - 동기 : snapshot
  - 비동기: rx

```typescript
this.name = this.route.snapshot.paramMap.get('name');
```

```typescript
this.route.paramMap.subscribe(el => {
  this.name = el.get('name');
});
```



### - QueryParams 설정 및 컴포넌트에서 사용하는 방법

- Routes에서는 설정 필요없음.
- 사용하려는 컴포넌트에서 ActivatedRoute 서비스 주입
- 주입된 서비스의 queryParamMap을 이용해서 query 겟또.
  - 동기 : snapshot
  - 비동기: rx

