# Angular Material



## 설치

```
ng add @angular/material
```



### `ng add` 명령어는 다음과 같은 일을 수행한다.

- `package.json` 에 의존성 설치
- `index.html` 에 Roboto 폰트 추가
- `index.html` 에 Material design icon 폰트 추가
- `style.less` 에 css 추가



## 사용법

- 사용할 컴포넌트를 `@NgModule` 에 import해서 사용

  - MatButtonModule을 import 한 뒤,

    ```
    import { MatButtonModule } from '@angular/material'
    ```

    

  - `@NgModule` 에 imports한다.

    ```
    @NgModule({
    	...
    	imports: [
    		MatButtonModule
    	],
    	...
    })
    ```


    이제 등록은 끝났다.

  - 사용하려는 컴포넌트에서 사용하면 된다.

    ```
    <button mat-raised-button color="warn">WARN</button>
    ```

    