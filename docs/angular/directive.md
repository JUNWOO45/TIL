# Directive



디렉티브는 크게 3가지 정도로 나눌 수 있다.

- 컴포넌트
  - 템플릿이 있는 디렉티브
- Structural(구조) 디렉티브
  - 템플릿에 DOM을 추가하거나 제거(템플릿의 구조를 변경하는거.)
  - ngFor, ngIf, ngSwitch
- 어트리뷰트 디렉티브
  - DOM의 모양과 동작을 수정
  - [ngModel], [ngClass], [ngStyle]



---

## 커스텀 어트리뷰트 디렉티브 만들어보기



CLI를 사용해서 디렉티브를 생성한다.

```
ng g d highlight
```

다음과 같이 생성된다.

```typescript
import { Directive } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor() { }
}
```

HostListener를 사용할건데ㅡ, DOM이벤트를 수신대기하는 데코레이터이다.

그리고 ElementRef를 사용해서 DOM 엘리먼트를 가져올거다.

```typescript
import { Directive } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(el: ElementRef) { }
  
  @HostListener('mouseenter') onMouseEnter() {
    this.highlight('blue');
  }
  
  @HostListener('mouseleave') onMouseLeave() {
    this.highlight(null);
  }
  
  highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
```

그리고 템플릿에 디렉티브 셀렉터를 넣어준다.

```html
<div appHighLight>
  여기에 마우스를 올렸다 내려놓으면 하이라이트가 생겨요..!
</div>
```



