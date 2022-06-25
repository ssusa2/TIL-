<!-- @format -->

## Set 객체

---

<br/>
Set 객체는 **중복되지 않는 유일한 값들의 집합**이다.

<br/>

### **특징**

- 동일한 값을 중복하여 포함하지 않는다.
- 요소 순서가 의미가 없다.
- 인덱스로 요소에 접근하지 못한다.

수학적 집합을 구현하기 위한 자료구조이다.

---

<br/>

### **Set 객체 생성**

```js
const set = new Set();
console.log(set); // Set(0) {}
```

```js
const set = new Set([1, 2, 2, 3, 3, 4]);
console.log(set); // Set(4) {1,2,3,4}
```

### **Set 객체의 특성을 이용한 배열 중복요소 제거하기**

```js
const uniq = (array) => [...new Set(array)];
console.log(uniq([2, 2, 2, 2, 1, 3, 3])); // [2,1,3]
```

### **Set 객체 요소 개수 확인하기**

```js
const { size } = new Set([2, 1, 3, 3, 4]);
console.log(size); // 4

const set = new Set([2, 1, 3, 3, 4]);
console.log(set.size); // 4
```

### **Set 객체 요소 추가하기**

```js
const set = new Set();
console.log(set);

set.add(1);
console.log(set); // 1

//add()뒤에 add()메서드 추가 가능
set.add(2).add(3);
console.log(set); // 3

// 하지만 증복된 요소는 추가되지 않는다.
set.add(4).add(4);
console.log(set); // 4
```

```js
const set = new Set();

set
	.add(1)
	.add('a')
	.add(true)
	.add(undefined)
	.add(null)
	.add({})
	.add([])
	.add(() => {});

console.log(set);
// Set(8) {1, 'a', true, undefined, null, {}, [], () => {}}
```

### **Set 객체 요소 존재 여부 확인하기**

```js
const set = new Set([1, 2, 3, 4]);

console.log(set.has(2)); // true
console.log(set.has(5)); // false
```

### **Set 객체 요소 삭제하기**

```js
const set = new Set([1, 2, 3]);

// 요소 3를 삭제한다.
set.delete(3); // true
```

### **Set 객체 요소 모두 삭제하기**

```js
const set = new Set([1, 2, 3]);

set.clear(); // undefined
console.log(set); // Set(0) {}
```

### **Set 객체 요소 순회하기**

```js
const set = new Set([1, 2, 3]);

set.forEach((v, v2, set) => console.log(v, v2, set));

// 1 1 Set(3) {1, 2, 3}
// 2 2 Set(3) {1, 2, 3}
// 3 3 Set(3) {1, 2, 3}
```
