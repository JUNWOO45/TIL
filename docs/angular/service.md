# 서비스



- 컴포넌트 또는 다른 서비스에서 사용하는 재사용가능한 기능의 집합
- 컴포넌트나 모듈에 주입해서 사용한다.



## 의존성 주입 : Dependency Injection

### "A컴포넌트에서 B 서비스를 사용한다"

- A에서 B의 인스턴스를 직접 생성해서 사용하는 것이 아니다.
- A에서 B를 주입하면, Angular가 자동으로 객체를 만들어서 사용할 수 있도록 처리한다.
  - 컴포넌트에 서비스를 주입
  - 모듈에 서비스를 주입
    - 모듈에 있는 모든 컴포넌트에서 같은 서비스를 사용.
- "A컴포넌트에 B서비스를 주입한다." 라고 표현한다.



---



## @Injectable 에서 지정

서비스는 단순한 자바스크립트 클래스에 불과합니다.

 `@Injectable` 데코레이터를 붙여서 Angular 서비스로 지정하는 것 뿐입니다.

`@Injectable` 데코레이터에는 `providedIn` 프로퍼티가 있는데, 이 프로퍼티를 사용하여 서비스 프로바이더의 범위를 지정할 수 있습니다.

아래 예시의 providedIn: 'root' 는, 이 서비스가 최상위 인젝터에 위치한다는 뜻입니다.

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LogService {

  constructor() { }
}
```



- `root` 는 root 모듈을 의미.
  - app module.
  - 이 서비스는 app module에 provide로 등록된다. 정도의 의미.
  - app module의 providers에 직접 등록 한 것이 아니라.

- 앵귤러는 이렇게 서비스를 싱글턴으로 사용한다.
  - https://angular.kr/guide/singleton-services



### 이런식으로 최상위 인젝터에 서비스 프로바이더를 등록하면, 이 서비스는 앱 전역에서 사용가능합니다.



---

또한, 다음과 같이 특정 @NgModule에 포함되도록 서비스를 등록할 수 있습니다.

```typescript
import { Injectable } from '@angular/core';
import { HomeModule } from './home.module';

@Injectable({
  providedIn: HomeModule,
})
export class HomeService {
  ...
}
```

이러한 방법은, HomeModule을 로드하지않으면 HomeService또한 사용할 수 없습니다.

즉, 실제 사용하지 않는 서비스는 자동으로 트리 셰이킹이 됩니다.

---

반대로, 모듈 안에 서비스 프로바이더를 등록하는 방법도 있습니다.

```typescript
import { NgModule } from '@angular/core';

import { UserService } from './user.service';

@NgModule({
  providers: [UserService],
})
export class UserModule {
}
```



이러면, 프로바이더의 범위를 컴포넌트 안으로 제한하게됩니다.

이러면 NgModule의 프로바이더와는 별개로, 컴포넌트 프로바이더가 의존성 객체를 생성합니다.

즉, 서비스의 인스턴스가 각각 생성되어서 이 서비스를 사용해 어떤 동작을 하더라도 같은 서비스를 사용하는 다른 컴포넌트는 영향을 받지 않습니다.



### Reference

- https://angular.kr/guide/providers

