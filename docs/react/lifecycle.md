# React Lifecycles

주로 많이 사용되는 라이프사이클에 대한 간략한 설명이다.

> constructor -> render -> ref -> componentDidMount -> (setState 또는 props 바뀔 때) -> shouldComponentUpdate -> render -> componentDidUpdate -> ... -> componnetWillUnmount -> 소멸

## constructor

- Good place to do one-time setup

## render

- Avoid doing anything besides returning JSX

\- Content visible on screen -

## componentDidMount

- Good place to do data-loading!
- 해당 컴포넌트가 렌더링되는 최초 1회 실행!
- 비동기 요청을 많이 한다.
  - ex) setInterval 작업을 해주고... `componentWillUnmount` 에서 해당 작업을 clearInterval해주는 식.

```javascript
class Test extends Component {
  ...
  interval;
	...
  
  componentDidMount() {
    this.interval = setInterval(() => {
      console.log('123');
    }, 1000);
  }

	...
  
  componentWillUnmount() {
		clearInterval(this.interval);
  }
}
```



\- Sit ad wait for updates-

## componentDidUpdate

- Good place to do more data-loading when state/props change

\- Sit and wait until this component is no longer shown

## componentWillUnmount

- Good place to do cleanup

<br>

그리고 비교적 덜 사용되는 라이프사이클들도 있다.( ... 는 주관적인 정보일듯)

`shouldComponentUpdate`

`getDerivedStateFromProps`

`getSnapshotBeforeUpdate`

<br>

---

## hooks에서의 라이프사이클(TBD)

```javascript
componentDidMount() {
  this.setState({
    name: 'junwoo',
    age: 100,
    result: 1
  });
}

...

useEffect(() => {
  setName('junwoo');
  setAge(100);
}, [name, age]);

useEffect(() => {
  setResult(1);
});
```



