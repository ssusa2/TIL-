<!-- @format -->

## Promise

<br/>
비동기 처리를 위한 ES6에서 도입된 프로미스에 대해 알아보자.
<br/>

---

데이터를 요청하는 함수가 실행되고 데이터를 받아오기도 전에 데이터를 보여주려고하면 오류가 발생하거나 빈 화면이 출력되는 현상이 발생하는 이를 해결하기 위한 방법 중 하나가 **프로미스**입니다.

---

### 프로미스의 3가지 상태

- **Pending 대기** - 비동기 처리 로직이 아직 완료되지 않은 상태
- **Fulfilled 이행** - 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- **Rejected 실패** - 비동기 처리가 실패하거나 오류가 발생한 상태

#### **Pending**

```js
new Promise(); // -> 대기 상태
```

new Promise() 를 호출할 때, 콜백함수를 선언할 수 있고 인자는 resovle , reject 이다.

```js
new Promise(function (resolve, reject) {
	// ...
});
```

#### **Fulfilled**

콜백 함수의 인자 **resovle** 를 아래와 같이 실행하면 이행 상태가 된다.

```js
new Promise(function (resolve, reject) {
	resolve();
}); // -> 이행 상태
```

이행 상태가 된다면 then() 을 이용하여 처리 결과값을 받을 수 있다.

```js
function getData() {
	return new Promise(function (resolve, reject) {
		var data = 100;
		resolve(data);
	});
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function (resolvedData) {
	console.log(resolvedData); // 100
});
```

#### **Rejected**

new Promise() 로 프로미스 객체를 생성하면 인자로 resolve 와 reject 를 사용할 수 있다. 여기서 reject 를 아래와 같이 사용한다면 실패 상태가 된다.

```js
new Promise(function (resolve, reject) {
	reject();
});
```

그리고 실패 상태가 된다면 실패한 이유로 실패 처리의 결과값을 catch()로 받을 수 있다.

````js
function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function(err) {
  console.log(err); // Error: Request is failed
});```
````

---

### **프로미스의 에러 처리 방법**

1. **then() 의 두 번 째 인자로 에러를 처리하는 방법**

```js
function getData() {
	return new Promise(function (resolve, reject) {
		reject('failed');
	});
}

// 1. then()의 두 번째 인자로 에러를 처리하는 코드
getData().then(
	function () {
		// ...
	},
	function (err) {
		console.log(err);
	}
);

// 2. catch()로 에러를 처리하는 코드
getData()
	.then()
	.catch(function (err) {
		console.log(err);
	});
```

then() 의 첫 번째 콜백 함수 내부에서 오류가 나는 경우 오류를 제대로 잡아내지 못하는 경우가 있다.

```js
// then()의 두 번째 인자로는 감지하지 못하는 오류
function getData() {
	return new Promise(function (resolve, reject) {
		resolve('hi');
	});
}

getData().then(
	function (result) {
		console.log(result);
		throw new Error('Error in then()'); // Uncaught (in promise) Error: Error in then()
	},
	function (err) {
		console.log('then error : ', err);
	}
);
```

2. **catch() 를 이용하는 방법**

```js
// catch()로 오류를 감지하는 코드
function getData() {
	return new Promise(function (resolve, reject) {
		resolve('hi');
	});
}

getData()
	.then(function (result) {
		console.log(result); // hi
		throw new Error('Error in then()');
	})
	.catch(function (err) {
		console.log('then error : ', err); // then error :  Error: Error in then()
	});
```

<img src="https://joshua1988.github.io/images/posts/web/javascript/catch-handling-error.png"/>

때문에 then() 의 두 번째 인자로 에러를 처리하는 방법보다는 catch()를 이용하는 방법을 사용하는 게 좋겠다.
