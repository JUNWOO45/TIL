<h1>
  express-generator에 nodemon 적용하기
</h1>



1.nodemon을 development dependency로 설치했습니다.

```
$ npm install --save-dev nodemon
```

2.package.json을 확인해보면...

```
"scripts": {
	"start": "node ./bin/www"
}
```

으로 설정되어 있는 것을 볼 수 있습니다.

이 부분이 npm start인 것이라고 합니다.

노드의 실행은 node 어쩌구.js 로 실행하는데,

npm start를 하면, "node ./bin/www"가 실행되는 것입니다.

특이하게도 www는 확장자가 없지만, js파일인 것을 눈치챌 수 있습니다!

3.nodemon을 실행하기 위해서 script 부분을 다음과 같이 수정합니다.

```
"scripts": {
	//"start": "node ./bin/www"
	"start": "nodemon ./bin/www"
}
```

4.

```
$ npm start
는 이제 다음과 같습니다!
$ nodemon ./bin/www
```





<h2>
  궁금증
</h2>

```
저장을 하면 바로 반영이되는 live server?는 어떻게 수정하는 걸까??

```





도움받은 곳!

- https://www.freecodecamp.org/forum/t/nodemon-with-express-generator/236425
- https://stackoverflow.com/questions/23647593/nodemon-express-listen-port

