# innerHTML바인딩할 때 스타일이 적용안되는 문제



innerHTML 속성으로 바인딩 할 경우, 스타일이나 클래스가 사라지는 현상이 생겼다.

버그는 아니라고 한다.

[https://blog.eunsatio.io/develop/Angular-2%2B-innerHTML%EC%97%90%EC%84%9C-%EC%9D%B8%EB%9D%BC%EC%9D%B8-%EC%8A%A4%ED%83%80%EC%9D%BC%EC%9D%B4-%EC%97%86%EC%96%B4%EC%A7%88-%EB%95%8C](https://blog.eunsatio.io/develop/Angular-2%2B-innerHTML에서-인라인-스타일이-없어질-때)



파이프를 만들어서 해결하는 방법이 있다고 하지만, 우리 프로젝트에서는 외부 lib을 가져와서인지, 잘 되질 않았다.

그래서 이 방법으로 수정.

`DomSanitizer` 를 사용하는 방법인데, 얘는 Cross Site Scripting Security bugs (XSS) 를 방지해준다.

보안을 위한 설정이기때문에 마구잡이로 사용해서는 안될듯하다.

https://stackoverflow.com/questions/50183294/angular-add-style-tag-into-innerhtml



Ref

-  [https://blog.eunsatio.io/develop/Angular-2%2B-innerHTML%EC%97%90%EC%84%9C-%EC%9D%B8%EB%9D%BC%EC%9D%B8-%EC%8A%A4%ED%83%80%EC%9D%BC%EC%9D%B4-%EC%97%86%EC%96%B4%EC%A7%88-%EB%95%8C](https://blog.eunsatio.io/develop/Angular-2%2B-innerHTML에서-인라인-스타일이-없어질-때)
- https://stackoverflow.com/questions/50183294/angular-add-style-tag-into-innerhtml