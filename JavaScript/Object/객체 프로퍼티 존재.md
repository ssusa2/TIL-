<!-- @format -->

## 객체 프로퍼티 존재 유무 확인하기

### 예시

```js
const obj = {
	name: 'suin',
	age: 18,
};
```

---

<br/>

### in 연산자

<br/>

문법

```js
프로퍼티 in 객체;
```

```js
console.log('name' in obj); //true
```

---

<br/>

### Reflect.has() 메서드

<br/>

문법

```js
Reflect.has(객체, 프로퍼티);
```

```js
console.log(Reflect.has(obj, name)); //true
```

---

<br/>

### hasOwnProperty()

<br/>

문법

```js
객체.hasOwnProperty(프로퍼티);
```

```js
console.log(obj.hasOwnProperty('name')); //true
```
