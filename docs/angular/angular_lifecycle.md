# Angular LifeCycle



## constructor

사실 생성자는 라이프사이클은 아니고 클래스 자체의 기능임.

즉, 생성자를 호출하는 주체가 앵귤러가 아니고 JS엔진.



비슷하다고 느낄수 있는 **ngOnInit** 은 생명주기 훅.

순수하게 앵귤러가 컴포넌트 초기화를 완료했다는 의미를 가진다.



예를 들어 `@Input()` 데코레이터를 사용하는 경우,

`Input()` 프로퍼티는 `ngOnInit` 안에서 접근 가능/ `constructor` 에서는 undefined.