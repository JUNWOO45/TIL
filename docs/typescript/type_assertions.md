# 타입 단언 Type Assertions

프로그래머가 타입스크립트보다 타입에 대해 더 잘 이해하고 있는 상황을 의미한다.

"타입스크립트야. 내가 타입을 알고있어. 나를 믿어봐!"

```typescript
function generateStr(value: string | number, isBoolean: boolean): string {
  if(isBoolean) {
    return value.toFixed(2);	
    // Property 'toFixed' does not exist on type 'string'.(2339)
  }
  
  return 'hmm... value is string';
}
```

isBoolean이 참일 경우, value는 number이고, Number.toFixed() 메소드를 상황하려는 상황이다.

하지만 타입스크립트는 `isBoolean` 이 참인지, 거짓인지를 컴파일 단계에서는 판단할 수 없기 때문에, `value` 타입이 string인지 number인지 추론할 수 없어서 에러를 반환한다.



```typescript
function generateStr(value: string | number, isBoolean: boolean): string {
  if(isBoolean) {
    return (value as number).toFixed(2);
  }
  
  return 'hmm... value is string';
}
```



따라서, `isBoolean` 이 참인 경우, `value` 타입이 number라고 **단언** 해야 한다.

다음과 같이 사용할 수도 있다.

```typescript
function generateStr(value: string | number, isBoolean: boolean): string {
  if(isBoolean) {
    return (<number>value).toFixed(2);
  }
  
  return 'hmm... value is string';
}
```

