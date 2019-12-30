# Angular LifeCycle



## constructor

사실 생성자는 라이프사이클은 아니고 클래스 자체의 기능임.

즉, 생성자를 호출하는 주체가 앵귤러가 아니고 JS엔진.



## ngOnInit

`constructor` 와 비슷하다고 느낄수 있는 **ngOnInit** 은 생명주기 훅.

순수하게 앵귤러가 컴포넌트 초기화를 완료했다는 의미를 가진다.



예를 들어 `@Input()` 데코레이터를 사용하는 경우,

`Input()` 프로퍼티는 `ngOnInit` 안에서 접근 가능/ `constructor` 에서는 undefined.



## ngOnChanges

`ngOnChanges` 도 최초에 동작하는구나.

아마 undefined에서 값이 할당될 때 동작하는듯ㅇㅇ

> ㄴㄴ.데코레이터가 달린 경우에만 불리움.
>
> 그 이유는, ngOnChanges는 상위에서 자신에게로 데이터가 들어올 때만 동작하는 라이프사이클임.



## ngDoCheck

기본적으로 `ngOnChanges` 와 같은 동작을 함.

근데 결정적이면서 엄청 중요한 차이

`ngOnChanges` 는 값이 완전히 바뀔때만 검사.

하지만 `ngDoCheck` 는 obj.property가 바뀌어도 검사함.

> 게다가 doCheck는 @Input처럼 데코레이터가 안달려도 검사하는것같다!?



---

간단한 정리가 있어서 기록으로 남긴다.

```
constructor : 가장 먼저.
ngOnChanges : 최초 초기화될때 + Input프로퍼티가 변경될 때
-> Input 데코레이터가 사용된 프로퍼티가 없으면 실행되지 않음.
ngDoCheck : 모든 데이터 변경을 감지
ngOnInit : 프로퍼티가 초기화된 직후
ngAfterViewInit : 템플릿이 모두 초기화되었을때
ngAfterViewChecked : 템플릿에 바인딩된 값이 변경되었을 때
```

