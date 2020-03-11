# Angular HTTP 통신



Vue나 React는 HTTP 통신을 할 때 써드파티 라이브러리를 사용한다.

ex: Axios...

하지만 Angular에는 모듈이 내장되어있다.

- HttpClientModule을 추가한다.
- HttpClient 서비스를 생성한다.
- 컴포넌트에 HttpClient 서비스를 주입한다.
- Promise 객체로 사용하기위해선 `toPromise()` 메소드를 사용한다.

---

`app.module.ts` 에서 `HttpClientModule` 을 imports 해야한다.

```typescript
@NgModule({
  ...
  imports: [
    HttpClientModule
  ],
  ...
})
export class AppModule {}
```



그리고 따로 생성한 서비스에서는 `HttpClient` 를 주입하고 메소드를 생성.

```typescript
@Injectable({
  providedIn: 'root'
})
export class AccountService {
  constructor(private http: HttpClient) { }

  getUsers() {
    return this.http.get('http://127.0.0.1:3000/account').toPromise();
  }
}
```



그리고,컴포넌트에서 해당 서비스를 주입받아 사용하는 식.

```typescript
@Component({
  selector: 'app-account',
  templateUrl: './account.component.html',
  styleUrls: ['./account.component.less']
})
export class AccountComponent implements OnInit {
  userData: Account[];

  constructor(private account: AccountService) { }

  async ngOnInit() {
    this.userData = await this.account.getUsers();
  }
}
```

