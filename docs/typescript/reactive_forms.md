# Reactive Forms



## Form Control

```typescript
const myFormControl = new FormControl();
```

Form Control을 생성할 때 arguments를 constructor에 pass할 수 있다.

```typescript
const myFormControl = new FormControl({
  { value: 'Hello Form Control!', disabled: true },
	[ Validators.required, Validators.maxLength(15)]
})
```



### 첫번째 Parameter는 FormState.

Form Control의 초기값과 disabled속성을 부여한다.

### 두번째 parameter는 Validators의 배열.

validation을 통과하지않으면 Form Control을 invalid하게 만든다.



## Form Group

Form Group은 Form Controls의 그룹이다.

혹은, nested Form Groups일 수 있다.

전체 그룹의 유효성에대한 정보를 가지고 있다.

```typescript
const formGroup = new FormGroup({
  'name': new FormControl('', [ Validators.required ]),
  'email': new FormControl('', [Validators.required]),
  'address': new FormGroup({
    'zipcode': new FormControl(''),
    'street': new FormControl(''),
    'detail': new FormControl('')
  })
})
```

위와같은 경우, Form Group은 name과 email 프로퍼티가 채워져야만 유효하다.(required하기 때문.)



컴포넌트 안에 Form Group을 만들었다면, 이제 HTML에 바인딩시킬 수 있다.

```html
<form [formGroup]="formGroup">
  <h1>사용자 프로필 Form</h1>
  
  <input required type="text" placeholder="박준우" formControlName="name">
  
  <input required type="text" placeholder="이메일" formControlName="email">
  
  <div formGroupName="address">
    <input required type="text" placeholder="우편번호" formControlName="zipCode">
    
    <input required type="text" placeholder="도로명주소" formControlName="street">
    
    <input required type="text" placeholder="상세주소" formControlName="detail">
  </div>
</form>
```



## Form Control 읽기

Form Group의 메소드를 이용하면 특정한 Form Control의 값을 알거나 Form Control의 메소드를 사용할 수 있다.

```typescript
const getName = formGroup.get('name').value;

const getZipcode = formGroup.get('address.zipcode').value;
```

<br>

HTML에서는 이렇게도 사용가능하다.

```html
<div>
  이름 : {{ formGroup.get('name').value }}
</div>
<div>
  우편번호 : {{ formGroup.get('address.zipcode').value }}
</div>
```





## Form Array

Form Array는 Form control들이나 Form Group들, 혹은 Form Array들의 집합이다.

```typescript
const formGroup = new FormGroup({
  'phones': new FormArray([
    new FormGroup({
      'number': new FormControl('', [ Validators.required ]),
      'type': new FormControl('Primary')
    }),
    new FormGroup({
      'number': new FormControl(''),
      'type': new FormControl('Secondary')
    })
  ])
})
```



HTML에는 다음과 같겠지.

```html
<form [formGroup]="formGroup">
  <h1>
    전화번호
  </h1>
  
  <div 
       class="phones"
       *ngFor="let phoneList of formGroup.get('phones')['controls'] let i = index"
       formArrayName="phones">
    <ng-container [formGroupName]="i">
      <p>
        Phone Type:  {{ phoneList.get('type').value }}
      </p>
      
      <input
             type="tel"
             placeholder="전화번호"
             formControlName="number">
    </ng-container>
  </div>
</form>
```



## Form Value 업데이트하기



### setValue

setValue와 patchValue 메소드를 사용해서 Form Group Controls의 값을 설정할 수 있다.

setValue 메소드를 사용할땐, 모든 Form Group의 프로퍼티가 들어있는 complete한 object를 넘겨주어야한다. 그렇지않으면 에러.

```typescript
const formGroup = new FormGroup({
  'name': new FormControl('', [ Validators.required ]),
  'email': new FormControl('', [ Validators.required]),
  'address': new FormGroup({
    'zipcode': new FormControl(''),
    'street': new FormControl(''),
    'number': new FormControl(''),
  })
});

const updatedUserInfo = {
  'name': 'junwoo park',
  'email': 'junwoo45@jaranda.kr',
  'address': {
    'zipcode': '123123',
    'street': '동탄중앙로',
    'number': 1234
  }
}

formGroup.setValue(updatedUserInfo);
```



### patchValue

반면에, patchValue 메소드는 내가 명시한 프로퍼티만 덮어쓰기가 가능하다.

```typescript
const formGroup = new FormGroup({
  'name': new FormControl('', [ Validators.required ]),
  'email': new FormControl('', [ Validators.required]),
  'address': new FormGroup({
    'zipcode': new FormControl(''),
    'street': new FormControl(''),
    'number': new FormControl(''),
  })
});

const newUserAddress = {
  'zipcode': '456456',
  'street': '판교역로',
  'number': 44332211
};

formGroup.patchValue({
  'address': newUserAddress
});
```



한가지 알아야 할 점은, setValue 메소드는 Form Groups는 물론 Form Controls에서도 사용가능하다는 점이다.

```typescript
formGroup.get('email').setValue('abcabc@gmail.com');
```



## Form Validation Status

간단하다.

하나의 Form Control의 Validation이 유효하지 못하면, 당연히 해당 Form Group의 Validation도 유효하지 못하다.

```typtescript
const isFormValid = formGroup.valid;
//FormGroup 유효성 검사

const isNameValid = formGroup.get('name').valid;
//개별적인 Form Control 유효성 검사
```



## 변화 감지하기

굉장히 흥미로운 부분.

Form Groups나 Form Controls의 변화를 subscribe하여 감지해낼 수 있다.

```typescript
formGroup.valueChanges.subscribe(val => {
  //Insert Logics!
})
```

다음은 좀 더 현실적인 예.

```typescript
formGroup.get('address.zipcode').valueChanges
	.subscribe(async (val) => {
	  const fullAddress = await _service.getFullAddress(val);
  
	  formGroup.get('address.street').setValue(fullAddress.street);
})
```

