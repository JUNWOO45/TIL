

<h1>Promise</h1>

- Promise?

```
자바스크립트 비동기 처리에 사용되는 객체
```



- 간단한 ajax통신 코드

```
function getData(cbFunc) {
    $.get("url주소", function(response) {
        cbFunc(response);
    });
}

getData(function(tableData) {
    console.log(tableData);
    //response값이 tableData로 전달되고 있습니다.
});
```

- 이러한 코드에 프로미스를 적용시켜본다면,

```
function getData(cbFunc) {
    return new Promise(function(resolve, reject) {
        $.get("url주소", function(response) {
            resolve(response);
        });
    });
}

getData().then(function(tableData) {
    console.log(tableData);
});
```

이런식으로 바뀝니다.



<h3>프로미스의 3가지 상태</h3>

new Promise()로 프로미스를 생성하고 종료될때까지 3가지 상태를 갖습니다.

1) pending : 비동기 처리 로직이 아직 완료되지않은 상태

2) fulfilled : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태

3) rejected : 비동기 처리가 실패하거나 오류가 발생한 상태 



- pending

new Promise()메서드를 호출하면 pending상태가 됩니다.

```
new Promise();
```

new Promise()메서드를 호출할때, 콜백함수의 인자로 resolve, reject

```

```

- fulfilled

콜백함수의 인자 resolve를 실행하면 fulfilled상태가 됩니다.

```
new Promise(function(resolve, reject) {
    resolve();
});
```

fulfilled상태가되면 then()을 이용하여 처리 결과값을 받을 수 있구요.

```
function getData() {
    return new Promise(function(resolve, reject) {
        var name = "junwoo";
        resolve(name);
    });
}

getData().then(function(resolvedName) {
    console.log(resolvedName);	// "junwoo"
});
```

- rejected

프로미스 객체의 콜백 함수 인자로 받는 reject인자로 reject()메서드를 실행하면 rejected상태가 됩니다.

```
new Promise(function(resolve, reject) {
    reject();
});
```

rejected상태가 되면 catch()로 받을 수 있습니다.

```
function getData() {
    return new Promise(function(resolve, reject) {
        reject(new Error("요청 실패!"));
    });
}

getData().then().catch(function(err) {
    console.log(err);	//"요청 실패!"
});
```



<h3>
    Promise Chaining
</h3>

```
function getData() {
    return new Promise(function(resolve, reject) {
        setTimeout(function() {
            resolve(10);
        }, 1000);
    });
}

getData().then(function(result) {
    console.log(result);	//10
    return result + 100;
}).then(function(result) {
    console.log(result);	//110
    return result + 1000;
}).then(function(result) {
    console.log(result);	//1110
});
```



<h3>
    Promise 에러 처리 방법
</h3>

2가지 방법이 있습니다.

1) then()의 두번째 인자로 에러를 처리하는 방법

```
getData().then(
	handleSucess,
	handleError
);
```

2) catch()를 이용하는 방법

```
getData().then().catch();
```



위에서 살펴본 두가지 방법 모두 reject()메서드가 호출되어 rejected상태가 되었을 경우에 실행이 됩니다.

예시를 살펴보겠습니다.

```
function getData() {
    return new Promise(function(resolve, reject) {
        reject("failed!!");
    });
}

//1) then()으로 에러를 처리하는 방법
getData().then(function() {
    //...
}, function(err) {
    console.log(err);	//"failed!!"
})

//2) catch()로 에러를 처리하는 방법
getData().then().catch(function(err) {
    console.log(err);	//"failed!!"
})
```

