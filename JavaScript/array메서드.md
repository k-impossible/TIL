### 추가, 삭제

* push : 배열 끝에서 추가
* pop : 배열 끝에서 삭제
* unshift : 배열 맨 앞에서 추가
* shift : 배열 맨 앞에서 삭제
* splice : 지정하는 배열 포지션에서 추가,삭제,교체
```javascript
let arr = [1,2,3,4]

arr.push("a") // return : "a" (추가된 값)
console.log(arr) // [1,2,3,4,"a"]

arr.pop() // return : "a" (삭제된 값)
console.log(arr) // [1,2,3,4]

arr.unshift(0) // return : 5 (배열 길이)
console.log(arr) // [0,1,2,3,4]

arr.shift() // return : 0 (삭제된 값)
console.log(arr) // [1,2,3,4]

// splice 교체
arr.splice(2,1,"a","b") // return : [3] (사라지는 값이 들어간 새로운 배열)
console.log(arr) // [1,2,"a","b",4]

// splice 삭제
arr.splice(2,3) // return : ["a","b"] (사라지는 값이 들어간 새로운 배열)
console.log(arr) // [1,2]

// splice 추가
arr.splice(2,0,3,4) // return : [] (사라지는 값이 들어간 새로운 배열)
console.log(arr) // [1,2,3,4]
```
`추가,삭제 시 push,pop은 배열 마지막에서 동작하는 반면 shift, unshift는 배열 맨 앞에서 동작하기 때문에 배열 전체 요소들이 이동해야 하므로 효율이 좋지 않다.`

<br>

### 존재, 위치확인
* includes : 배열에서 해당 인자의 포함 여부를 반환
* indexOf : 배열 첫번째 부터 해당 인자를 검색해 인덱스 값 반환
* lastIndexOf : 배열 마지막 부터 해당 인자를 검색해 인덱스 값 반환
```javascript
const array = ['a', 'b', 'c', 'a'];

console.log(array.includes('a')); // true
console.log(array.includes('z')); // false

console.log(array.indexOf('a')); // 0
console.log(array.indexOf('z')); // -1

console.log(array.lastIndexOf('a')); // 3    
```

<br>

### concat()
배열이나 값들을 기존 배열에 합쳐서 새로운 배열을 반환
```javascript
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const str = "g"

const array3 = array1.concat(array2);
const array4 = array3.concat(str);

console.log(array3); // [ 'a', 'b', 'c', 'd', 'e', 'f' ]
console.log(array4); // [ 'a', 'b', 'c', 'd', 'e', 'f' , 'g']
```

<br>

### join()
배열의 모든 요소를 하나의 문자열로 변환
```javascript
const array = ['k', 'i', 'm'];

console.log(array.join()) // "k,i,m"
console.log(array.join("")) // "kim"
console.log(array.join(" - ")) // "k - i - m"
```

<br>

### split()
문자열을 구분자로 나눠 배열로 반환
```javascript
const str = "k,i,m";
const array = str.split(",");
const array2 = str.split(",",1);

console.log(array) // ['k', 'i', 'm']
console.log(array) // ['k']
```

<br>

### reverse()
배열 요소의 순서를 거꾸로 바꾼 배열 반환
```javascript
const array = [1, 2, 3, 4, 5]
const result = array.reverse();

console.log(array) // [ 5, 4, 3, 2, 1 ]
console.log(result) // [ 5, 4, 3, 2, 1 ]
```

<br>

### slice()
배열에서 지정한 시작,끝 위치의 요소들을 새로운 배열로 반환
```javascript
const array = [1, 2, 3, 4, 5]
const result = array.slice(2,4)

console.log(array) // [ 1, 2, 3, 4, 5 ]
console.log(result) // [ 3, 4 ]
```
`splice()와 비슷하게 동작하지만 splice()는 원본 배열을 변경시킴`

<br>

### find()
콜백 함수 내 조건에 만족하는 첫번째 배열 요소의 값을 즉시 반환
```javascript
const array = [10, 251, 369, 4000, 54];
const result = array.find(element => element > 1000);

console.log(result) // 4000
```
`만족하는 요소가 없다면 undefined 반환`

<br>

### filter()
콜백 함수 내 조건에 만족하는 모든 배열 요소를 새로운 배열로 반환
```javascript
const array = [10, 251, 369, 4000, 54];
const result = array.filter(element => element < 100);

console.log(result) // [ 10, 54 ]
```
`어떤 요소도 만족하지 못하면 빈 배열 반환`

<br>

### map()
모든 배열 요소에 대해 콜백 함수를 호출한 결과를 모아서 새로운 배열로 반환
```javascript
const array = [10, 250, 366, 4000, 54];
const result = array.map(element => element / 2);

console.log(result) // [ 5, 125, 183, 2000, 27 ]
```

<br>

### some()
콜백 함수 내 조건에 만족하는 배열 요소가 하나라도 있으면 true 반환, 없으면 false 반환
```javascript
const array = [10, 250, 366, 4000, 54];
const result = array.some(element => element < 50);
const result2 = array.every(element => element < 500);

console.log(result) // true
console.log(result2) // false
```
`every()는 모든 배열 요소가 조건에 만족해야 true 반환`

<br>

### reduce()
배열 요소에 대해 콜백 함수의 계산값을 누적한 값을 반환
```javascript
const array = [10, 25, 30, 45, 50];
const result = array.reduce((prev,current) => prev + current);
const result2 = array.reduce((prev,current) => prev + current,5);

console.log(result) // 160
console.log(result) // 165
```
* prev : 누적 값이 저장되는 인자
* current: 처리할 현재 배열 요소
* 콜백 최초 호출 시, initialValue를 제공한 경우 prev는 initialValue와 같고 current는 배열의 첫번째 값과 같다. 제공하지 않았다면 prev는 배열의 첫번째 값과 같고 current는 배열의 두번째 값과 같다.
* reduceRight()는 배열의 마지막 부터 계산을 진행한다.

<br>


>[MDN - JavaScript Array](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array)
