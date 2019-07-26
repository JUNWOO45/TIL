# LESS

LESS는 CSS에 Script능력(변수, 함수, 연산, 중첩, 스코프 등)을 덧붙여 확장한 언어입니다.

LESS는 클라이언트 또는 서버환경(node.js)에서 모두 실행가능합니다.

CSS Preprocessor(CSS 전처리기)로서 쉽고 빠르고 체계적으로 프로그래밍할 수 있도록 해줍니다!



<h2>
  Variables
</h2>

```css
@width: 100px;
@height: @width - 50px;

.test1 {
  width: @width;
  height: @height;
}
```

Outputs:

```css
.test1 {
  width: 100px;
  height: 50px;
}
```



## Mixins

```css
.bordered {
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}

.test2 {
  color: red;
  .bordered();
}

.test3 {
  color: blue;
  .bordered();
}
```

Output:

```css
.bordered {
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}

.test2 {
  color: red;
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}

.test3 {
  color: blue;
  border-top: 1px dotted black;
  border-bottom: 2px solid pink;
}
```

> 믹스인을 **호출**할 때, 괄호는 옵션입니다!
>
> .bordered(); === .bordered;

<h3>
  믹스인 출력 막기
</h3>

믹스인을 만들고는 싶지만, 그 믹스인을 지금 출력할 필요가 없을때에는 뒤에 괄호를 넣으면 됩니다.

```css
.my-mixin {
  //괄호가 붙지않은 믹스인은 컴파일됩니다!
  color: black;
}

.my-other-mixin() {
  //괄호가 붙은 믹스인은 css파일에 컴파일되지 않습니다!
  background-color: gray;
}

.demo {
  .my-mixin();
  .my-other-mixin();
}
```

Output:

```css
.my-mixin {
  color: black;
}

.demo {
  color: black;
   background-color: gray;
}
```

### 네임스페이스

```css
#outer {
  .inner {
    color: red;
  }
}

.other {
  #outer > .inner;
}
```

Output:

```css
#outer .inner {
  color: red;
}

.other {
  color: red;
}
```

> 모두 같은 결과입니다.
>
> \#outer > .inner;
>
> \#outer .inner;
>
> \#outer.inner;

<h2>
  Nesting
</h2>

```css
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
```

Output:

```css
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```

가상선택자를 사용할 수 있습니다.

**&기호는 바로 위의 부모 선택자를 가리킵니다!**

```css
.parent {
  display: block;
  color: red;
  &:hover {
    font-size: 50px;
    color: orange;
  }
}
```

Output:

```css
.parent {
  display: block;
  color: red;
}
.parent:hover {
  font-size: 50px;
  color: orange;
}
```



## Operations

```css
//숫자들은 같은 단위로 변환됩니다.
@conversion01: 5cm+10mm;	//6cm
@conversion02: 2 - 3cm - 5mm	//-1.5cm
  
//변환 불가능!
@imposibble01: 2 + 5px - 3cm;	// 4px

//example
@base: 5%;
@filler: @base * 2;	//10%
@other: @base + @filler //15%
```

```css
@var: 1px + 5 //6px
@width: (@var + 5) * 2;

.operation {
  width: @width;
  border: (@width / 11) solid black;
}
```

Output:

```css
.operation {
  width: 22px;
  border: 2px solid black;
}
```



---

```css
@front:#3c3e41;
@bgbasic:#f7f7f9;
@point:#a4c041;
@front1:rgba(11, 11, 11, 0.87);
@front2:rgba(0, 0, 0, 0.68);

.ne(){pointer-events:none;touch-action: none;}

.png(@p,@n){background-image:url('/assets/img/@{p}/@{n}.png');}
.svg(@p,@n){background-image:url('/assets/img/@{p}/@{n}.svg');}
.svgc(@n,@c){background-color: @c;-webkit-mask-image: url('/assets/img/icon/@{n}.svg');mask-image: url('/assets/img/icon/@{n}.svg');}
.gif(@p,@n){background-image:url('/assets/@{p}/@{n}.gif');}
.jpg(@p,@n){background-image:url('/assets/@{p}/@{n}.jpg');}
.cover(){object-fit:cover;}
.contain(){object-fit:contain;}
.bp(@p){background-position:@p;}
.bs(@s){background-size:@s;}
.ms(@s){-webkit-mask-size:@s;mask-size:@s;}
.bgsize(@c){-webkit-background-size:cover;-moz-background-size:cover;background-size:cover;}
.br(@r){-moz-border-radius:@r;-webkit-border-radius:@r;border-radius:@r;}

//size
.w(@w){width:@w;}
.w(@w) when (@w=fit-content){
    width:-webkit-fit-content;
    width:fit-content;
	width:-moz-fit-content;}
.h(@h){height:@h;}
.wh(@w,@h){.w(@w);height:@h;}
.whl(@w,@h){.w(@w);height:@h;line-height:@h;}
.whlh(@w,@h,@lh){.w(@w);height:@h;line-height:@lh;}
.maxwh(@w,@h){max-width:@w;max-height:@h;}
.maxh(@h){max-height:@h;}
.minh(@h){min-height:@h;}
.lh(@h){line-height:@h;}
.hl(@h){height:@h;line-height:@h;}
.hlh(@h,@lh){height:@h;line-height:@lh;}
//font
.fs(@s){font-size:@s;}
.fw(@w){font-weight:@w;}
.ls(@s){letter-spacing:@s;}
.tl(){text-align:left;}
.tc(){text-align:center;}
.tr(){text-align:right;}
.ti(@i){text-indent:@i;}
//margin
.mg(@t){margin:@t;}
.mgt(@m){margin-top:@m;}
.mgl(@m){margin-left:@m;}
.mgr(@m){margin-right:@m;}
.mgb(@m){margin-bottom:@m;}
//padding
.pd(@t){padding:@t;}
.pdt(@p){padding-top:@p;}
.pdl(@p){padding-left:@p;}
.pdr(@p){padding-right:@p;}
.pdb(@p){padding-bottom:@p;}
//border
.bd(@p,@c){border:@p solid @c;}
.bdl(@p,@c){border-left:@p solid @c;}
.bdr(@p,@c){border-right:@p solid @c;}
.bdb(@p,@c){border-bottom:@p solid @c;}
.bdt(@p,@c){border-top:@p solid @c;}
//position
.hide(){display:none;}
.show(){display:block;}

.ofh(){overflow:hidden;};
.ofa(){overflow:auto;}
.scrollx(){overflow-x:scroll;overflow-y:hidden;-webkit-overflow-scrolling: touch;}
.scrolly(){overflow-x:hidden;overflow-y:scroll;-webkit-overflow-scrolling: touch;}

.pa(){position:absolute;}
.pr(){position:relative;}
.fix(){position:fixed;}

.cb(){clear:both;}
.fl(){float:left;} 
.fr(){float:right;}
.fn(){float:none;}

.t(@t){top:@t;}
.b(@b){bottom:@b;}
.l(@l){left:@l};
.r(@r){right:@r};
.lr(@l,@r){left:@l;right:@r;}
.tb(@t,@b){top:@t;bottom:@b;}
.tblr(@t,@b,@l,@r){top:@t;bottom:@b;left:@l;right:@r;}
.full(){.tblr(0,0,0,0);}
//color
.c(@c){color:@c;}
.bc(@c){background-color:@c;}
.bg(@c){background:@c;}
.rgba(@r,@g,@b,@a){background-color:rgba(@r,@g,@b,@a);}
//filter
.dropshadowi(@p){-webkit-filter: drop-shadow(@p);-moz-filter: drop-shadow(@p); filter: drop-shadow(@p);}
.shadowi(@x,@y,@l,@c){-webkit-box-shadow: @x @y @l @c;-moz-box-shadow:@x @y @l @c;box-shadow:@x @y @l @c;}

.dropshadow(@p){/*-webkit-filter: drop-shadow(@p); filter: drop-shadow(@p);*/}
.dropshadow3(){.dropshadow(0 0 3px #e4e4e4);}
.dropshadow5(){.dropshadow(0 2px 3px #ccc);}
.bcshadow(@c){.c(#fff);.bc(@c);.dropshadow(0 0 3px @c);}
.shadow(@x,@y,@l,@c){/*-webkit-box-shadow: @x @y @l @c;-moz-box-shadow:@x @y @l @c;box-shadow:@x @y @l @c;*/}
.shadow1(){box-shadow: 0 8px 24px -7px rgba(11, 11, 11, 0.04), 0 6px 24px 5px rgba(11, 11, 11, 0.03), 0 24px 48px 0 rgba(11, 11, 11, 0.07);}
.shadow2(){box-shadow: 0 8px 22px 1px rgba(11, 11, 11, 0.06), 0 4px 8px 1px rgba(0,0,0,0.03),0 4px 7px -2px rgba(0,0,0,0.02);}
.shadow3(){box-shadow: 0 8px 16px -5px rgba(0, 0, 0, 0.02), 0 12px 24px 5px rgba(0, 0, 0, 0.03), 0 24px 48px 1px rgba(11, 11, 11, 0.06);}
.shadow4(){box-shadow: 0 4px 7px -2px rgba(0, 0, 0, 0.02), 0 4px 8px 1px rgba(0, 0, 0, 0.03), 0 8px 22px 1px rgba(11, 11, 11, 0.06);}
.shadow5(){box-shadow: 0 2px 8px -3px rgba(11, 11, 11, 0.04), 0 4px 8px 2px rgba(11, 11, 11, 0.04), 0 8px 22px 0 rgba(11, 11, 11, 0.08);}

.vm(){vertical-align:middle;}
.vb(){vertical-align:bottom;}
.vtb(){vertical-align:baseline;}
.z(@z){z-index:@z;}
.fit(){width:fit-content;height:fit-content;}
.iscroll(){-webkit-overflow-scrolling: touch;}
.center(){.pa();.mg(auto);.full();}
.hc(){.l(0);.r(0);.mg(auto);}
.vc(){top:0;bottom:0;margin:auto 0;}
.inline(){display:inline-block;}
.flex(){display: -webkit-flex;display: -ms-flexbox;display: flex;}
.wrap(@val){-webkit-flex-wrap:@val;-ms-flex-wrap:@val;flex-wrap:@val;}
.flex(@v){-webkit-flex:@v;-ms-flex:@v;flex:@v;}
.hand(){cursor:pointer;} 
.a(@a){opacity:@a;}
.s(@s){.wh(auto,auto);zoom:@s;}

.ultralight{.fw(200);}
.light{.fw(300);}
.normal{.fw(300);}
.bold(){.fw(900);}
.italic(){font-style:italic;}


.mask(@n){mask:url('/asset/@{n}.svg') no-repeat 50% 50%;-webkit-mask:url('/asset/@{n}.svg') no-repeat 50% 50%;}
.outline(@size, @color) {
	text-shadow: 0 0 @size @color;
	-moz-text-shadow: 0 0 @size @color;
	-webkit-text-shadow: 0 0 @size @color;
}
.click(){
	cursor:pointer;
	user-select: none;
	-moz-user-select: none;
	-khtml-user-select: none;
	-webkit-user-select: none;
	-o-user-select: none;
}
.card(){.pd(10px);.bc(#fff);.bdb(1px,#eee);}


.list(){.h(fit-content);.mg(0px auto);.ofa();}//아래로 스크롤하는 리스트

.align(@c){-webkit-align-items:@c;-ms-flex-align:@c;align-items:@c;}
.justify(@c){-webkit-justify-content:@c;-ms-flex-pack:@c;justify-content:@c;}



.flex(){display:flex;display:-webkit-flex;display:-ms-flexbox;}
.flex(@v){justify-content:@v;-webkit-justify-content:@v;-ms-flex-pack:@v;}
.fd(@v){-webkit-flex-direction:@v;-ms-flex-direction:@v;flex-direction:@v;}
.align(@v){-webkit-align-items:@v;-ms-flex-align:@v;align-items:@v;}
.brtl(@v){-webkit-border-top-left-radius:@v;-moz-border-radius-topleft:@v;border-top-left-radius:@v;}
.brbr(@v){-webkit-border-bottom-right-radius:@v;-moz-border-radius-bottomright:@v;border-bottom-right-radius:@v;}
.shadow(@v){-webkit-box-shadow: @v;-moz-box-shadow:@v;box-shadow:@v;}

.list(){
    >div{
        .card();
    }
}

.flex-column(){
	.flex();.justify(flex-start);
	>div{flex:auto;.tc();}
}


.flex-center(){
	display: flex;
	align-items: center;
	justify-content: center;
}
.nowrap(){white-space: nowrap;}
```

