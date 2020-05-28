# React Lifecycles

주로 많이 사용되는 라이프사이클에 대한 간략한 설명이다.

`constructor`

- Good place to do one-time setup

`render`

- Avoid doing anything besides returning JSX

\- Content visible on screen -

`componentDidMount`

- Good place to do data-loading!

\- Sit ad wait for updates-

`componentDidUpdate`

- Good place to do more data-loading when state/props change

\- Sit and wait until this component is no longer shown

`componentWillUnmount`

- Good place to do cleanup

<br>

그리고 비교적 덜 사용되는 라이프사이클이다.

`shouldComponentUpdate`

`getDerivedStateFromProps`

`getSnapshotBeforeUpdate`



