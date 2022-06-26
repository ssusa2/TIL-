<!-- @format -->

## Map 객체

---

<br/>

Map 객체는 **키와 값의 쌍으로 이루어진 컬렉션**이다.

<br/>

### **특징**

- 객체를 포함한 모든 값을 키로 사용할 수 있다.
- 이터러블
- 요소 개수(length)를 map.size()로 확인한다.

---

<br/>

### **Map 객체 생성하기**

```js
const map = new Map();
console.log(map); // Map(0) {}
```

Map 생성자 함수는 이터러블을 인수로 전달받아 Map객체를 생성한다.
이때, **이터러블은 키와 값의 쌍**으로 이루어져야 한다.
<br/>

````js
const map1 = new Map([
	['key1', 'value1'],
	['key2', 'value2'],
]);
console.log(map1); // Map(2) {'key1' => 'value1','key2' => 'value2'}```
````

키가 중복되면 값이 덮어써진다.

```js
const map = new Map([
	['key1', 'value1'],
	['key1', 'value2'],
]);
console.log(map); // Map(1) {'key1' => 'value2'}
```

<br/>

### **Map 객체 요소 개수 확인하기**

Map.prototype.size

```js
const { size } = new Map([
	['key1', 'value1'],
	['key2', 'value2'],
]);
console.log(size); // 2
```

size 프로퍼티로 요소 개수를 변경할 수 없다.

<br/>

### **Map 객체 요소 추가하기**

Map.prototype.set

```js
const map = new Map();
console.log(map); //Map(0) {}

map.set('key1', 'value1'); // Map(1){'key1' => 'value1'}
```

set메서드를 호출한 후에 연속적으로 호출할 수 있다.

```js
const map = new Map();
console.log(map); //Map(0) {}

map.set('key1', 'value1').set('key2', 'value2');

//Map(2){'key1' => 'value1', 'key2' => 'value2'}
```

**객체도 키값으로 사용할 수 있다.**

```js
const map = new Map();

const jung = { name: 'jung' };
const lim = { name: 'lim' };

// 객체도 키로 사용가능
map.set(jung, 'developer').set(lim, 'worker');

console.log(map);
//Map(2) { { name: 'jung' } => 'developer', { name: 'lim' } => 'worker'}
```

<br/>

### **Map 객체 요소 취득하기**

Map.prototype.get

```js
const map = new Map();

const jung = { name: 'jung' };
const lim = { lim: 'lim' };

// 객체도 키로 사용가능
map.set(jung, 'developer').set(lim, 'worker');

console.log(map.get(jung)); //'developer'
console.log(map.get('key')); //undefined
```

키를 갖는 요소가 없으면 undefined를 반환한다.

<br/>

### **Map 객체 요소 존재 확인하기**

Map.prototype.has

```js
const jung = { name: 'jung' };
const lim = { lim: 'lim' };

const map = new Map([
	[jung, 'developer'],
	[lim, 'worker'],
]);

console.log(map.has(jung)); // true
console.log(map.has('key')); // false
```

존재 여부를 불리언 값으로 반환한다.

### **Map 객체 요소 삭제하기**

Map.prototype.delete

```js
const jung = { name: 'jung' };
const lim = { lim: 'lim' };

const map = new Map([
	[jung, 'developer'],
	[lim, 'worker'],
]);

map.delete(jung); //true
console.log(map); //Map(1) {{ lim: 'lim' } => 'worker'}
```

연속적으로 호출할 수 없다.

### **Map 객체 요소 일괄 삭제하기**

Map.prototype.clear

```js
const jung = { name: 'jung' };
const lim = { lim: 'lim' };

const map = new Map([
	[jung, 'developer'],
	[lim, 'worker'],
]);

map.clear();
console.log(map); //Map(0){}
```

언제나 undefined를 반환한다.

### **Map 객체 요소 순회하기**

Map.prototype.forEach

<br/>
**콜백 함수에 전달하는 인수 3개**

1. 현재 순회 중인 요소값
2. 현재 순회 중인 요소키
3. 현재 순회 중인 Map 객체 자체

```js
const jung = { name: 'jung' };
const lim = { lim: 'lim' };

const map = new Map([
	[jung, 'developer'],
	[lim, 'worker'],
]);

map.forEach((v, k, map) => console.log(v, k, map));

/*
'developer' { name: 'jung' } Map(2) {
  { name: 'jung' } => 'developer',
  { lim: 'lim' } => 'worker'
  }
  
'worker' { lim: 'lim' } Map(2) {
  { name: 'jung' } => 'developer',
  { lim: 'lim' } => 'worker'
  }
*/
```

### **Map 객체의 메서드**

- keys 요소키를 값으로 갖는 이터레이터 반환(변수의 값)
- values 요소값을 값으로 갖는 이터레이터 반환(키와 값 형태의 값)
- entries 요소키와 요소값을 값으로 갖는 이터레이터 반환(변수의 값, 키와 값 쌍의 값)

```js
const jung = { name: 'jung' };
const lim = { lim: 'lim' };

const map = new Map([
	[jung, 'developer'],
	[lim, 'worker'],
]);

// keys()
for (const key of map.keys()) {
	console.log(key);
}
//{ name: 'jung' } { lim: 'lim' }

// values()
for (const value of map.values()) {
	console.log(value);
}
//'developer''worker'

// entries()
for (const entry of map.entries()) {
	console.log(entry);
}
//[ { name: 'jung' }, 'developer' ][ { lim: 'lim' }, 'worker' ]
```
