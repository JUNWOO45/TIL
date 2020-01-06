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

- cli로 생성

  - ng g s 서비스이름

    ```
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

  