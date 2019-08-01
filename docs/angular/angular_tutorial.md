# angular cli



## 설치

```
$ npm install -g @angular/cli
```



버전확인도 함 해쥬고..

```
$ ng version
```

## 프로젝트 생성

```
$ ng new <프로젝트명>
```



##컴포넌트 생성

```
$ ng generate component [컴포넌트 이름]
//줄여쓰기 가능
$ ng g c [컴포넌트 이름]
```

![angular1](../pic/angular2.png)

이렇게 폴더 안에 다 생성해 줄 뿐 아니라...

![angular2](../pic/angular1.png)



app.module.ts에 등록도 해쥼.. 귣..



## 특정 폴더 내에 컴포넌트 생성

```
$ ng g c section/time-display
```

![angular3](../pic/angular3.png)

이렇게 section 폴더 안에 time-display 폴더 생김

물론 module에도 등록이 되었습니다.



## 프로젝트 구조 간단하게 살펴보기

### app.module.ts

- 루트 모듈이라 생각하면 될 듯합니다.

  근간이 되는 모듈..

- `@NgModule` 안에 `declarations`, `exports`, `imports`, `providers`, `bootstrap` 등등..
  - declarations : "하나의 컴포넌트는 적어도 하나의 모듈안에 선언되어있어야 사용가능합니다."
  - imports: javascript module system의 그 imports.... 
  - exports: 상동.. exports를 사용하기위해서는 그렇다면 declarations 배열에 들어있어야겠네요.
  - bootstrap: 이 컴포넌트를 우선 시작하는듯.