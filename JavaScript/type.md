## 타입
자바스크립트에는 7가지 내장 타입이 있다.
null, undefined, boolean, string, number, object, symbol
값 타입은 `typeof` 연산자로 알 수 있다. 
하지만 반환값이 내장 타입과 정확히 매치되진 않는다.
```javascript
typeof undefined === "undefined" //true
typeof true === "boolean" //true
typeof 30 === "number" //true
typeof "30" === "string" //true
typeof {age: 30} === "object" //true
typeof Symbol() === "symbol" //true
```
 * null은 falsy한 유일한 원시 값이지만 타입은 object이다.
```javascript
typeof null === "object" //true
```
* function의 반환값을 보면 function이 내장 타입처럼 보이지만 실제로는 object의 하위 타입이다. 함수는 '호출 가능한 객체' 이다.
```javascript
typeof function a(){ ... } === "function" //true
```
* 배열은 숫자 인덱스를 가지며 추가 특성을 지닌 객체의 하위 타입이다.
```javascript
typeof [1,2,3] === "object" //true
```
* "undefiend"(값이 없는)과 "undeclared"(선언되지 않은)은 완전히 다른 개념이다. 
```javascript
let a;
a; // undefined
b; // Reference Error: b가 정의되지 않았습니다.

typeof a; // "undefined"
typeof b; // "undefined"
```
>"undefiend"는 접근 가능한 스코프에 변수가 선언되었으나 아무런 값도 없는 상태이고 "undeclared"는 접근 가능한 스코프에 변수 자체가 선언도 되지 않은 상태이다. 선언되지 않은 변수도 typeof하면 오류 처리를 하지않고 "undefiend"로 나온다.



<br>

## 원시 자료형
원시 자료형(primitve type)은 내장 타입 7가지 중에 object를 제외한 number, string, boolean, undefined, null, symbol 이 있다.
#### 특징
>* 원시 자료형을 변수에 할당하면 메모리 공간에 값 자체가 저장된다.
>* 원시 값을 갖는 변수를 다른 변수에 할당하면 원시 값 자체가 복사되어 전달된다.
>* 원시 자료형은 변경 불가능한 값(immutable value)이다. 한 번 생성된 원시 자료형은 읽기 전용 값이다.

```javascript
let num = 20;
let copiedNum = num;
let str = 'code';

console.log(num === copiedNum); // true

num = 30;
console.log(num === copiedNum); // false

console.log(copiedNum); // 20

str = 'states';
str[5] = 'z';

console.log(str); // states
```

<br>

## 참조 자료형
참조 자료형(reference type)은 원시 자료형이 아닌 모든 자료형을 말한다. 객체,배열,함수 등이 대표적인 참조 자료형이다.

#### 특징
>* 참조 자료형을 변수에 할당하면 메모리 공간에 주소값이 저장된다.
>* 참조 값을 갖는 변수를 다른 변수에 할당하면 주소값이 복사되어 전달된다.
>* 참조 자료형은 변경이 가능한 값(mutable value)이다.

```javascript
let arr = [0, 1, 2, 3];
let copiedArr = arr;
console.log(arr === copiedArr); // true

arr.push(4);
console.log(arr === copiedArr); // true

console.log(copiedArr); // [0, 1, 2, 3, 4]
```

<br>

## 얕은 복사, 깊은 복사
참조 자료형이 저장된 변수를 다른 변수에 할당할 경우, 두 변수는 같은 주소를 참조할 뿐 값 자체가 복사되지 않는다. 참조 자료형을 복사하여 똑같은 형태이지만 원본과 복사본이 서로 영향을 미치지 않는 방법이 있다.
#### 배열 복사
배열 내장 메서드인 slice()와 spread 문법(...)를 사용. 새로 생성된 배열은 원본 배열과 같은 요소를 갖지만 참조하는 주소는 다르기 때문에 복사본에 요소를 추가해도 원본에는 영향이 없다.
```javascript
let arr = [0, 1, 2, 3];
let copiedArr = arr.slice();
let copiedArr2 = [...arr];

console.log(copiedArr); // [0, 1, 2, 3]
console.log(arr === copiedArr); // false

console.log(copiedArr2); // [0, 1, 2, 3]
console.log(arr === copiedArr2); // false

copiedArr.push(4);
copiedArr2.push(4);

console.log(copiedArr); // [0, 1, 2, 3, 4]
console.log(copiedArr2); // [0, 1, 2, 3, 4]

console.log(arr); // [0, 1, 2, 3]
```

<br>

#### 객체 복사
객체 내장 메서드인 Object.assign()과 배열과 같이 spread 문법(...)을 사용해 복사할 수 있다.
```javascript
let obj = { firstName: "coding", lastName: "kim" };
let copiedObj = Object.assign({}, obj);
let copiedObj2 = {...obj};

console.log(copiedObj) // { firstName: "coding", lastName: "kim" }
console.log(copiedObj2) // { firstName: "coding", lastName: "kim" }

console.log(obj === copiedObj) // false
console.log(obj === copiedObj2) // false
```

<br>

#### 얕은 복사(shallow copy)
위 방법들  처럼 slice(), Object.assign(), spread 문법 등을 사용하면 참조 자료형의 값 자체를 복사 할 순 있지만 참조 자료형이 중첩된 구조라면 한 단계까지만 복사하고 그 내부 단계는 여전히 같은 주소값을 참조한다. 이것을 얕은 복사라고 한다.
```javascript
let users = [
	{
		name: "kimcoding",
		age: 26,
		job: "student"
	},
	{
		name: "parkhacker",
		age: 29,
		job: "web designer"
	},
];

let copiedUsers = users.slice();

console.log(users === copiedUsers); // false
console.log(users[0] === copiedUsers[0]); // true
```

<br>

#### 깊은 복사(deep copy)
참조 자료형 내부에 중첩되어 있는 모든 참조 자료형을 복사하는 것을 깊은 복사라고 한다. javascript의 다른 문법을 응용하면 깊은 복사와 같은 결과를 도출할 수 있다.

* JSON.stringify(), JSON.parse()
JSON.stringify()는 참조 자료형을 문자열 형태로 변환하여 반환하고 JSON.parse()는 문자열의 형태를 객체로 변환하여 반환한다.
중첩된 참조 자료형을 JSON.stringify()를 사용해 문자열 형태로 변환하고, 변환된 값에 JSON.parse()를 사용하면 깊은 복사와 같은 결과를 도출한다.
예외로, 중첩된 참조 자료형 중에 함수가 함수가 포함되있을 경우 함수가 null로 바뀌게 되어서 이 방법도 완전한 깊은 복사 방법은 아니다.
```javascript
const arr = [1, 2, [3, function(){ console.log('hello world')}]];
const copiedArr = JSON.parse(JSON.stringify(arr));

console.log(arr); 
// [1, 2, [3, function(){ console.log('hello world')}]]
console.log(copiedArr); // [1, 2, [3, null]]
console.log(arr === copiedArr) // false
console.log(arr[2] === copiedArr[2]) // false
```

<br>

* 외부 라이브러리 사용
완전한 깊은 복사를 해야 하는 경우라면 외부 라이브러리인 lodash, ramda를 설치해 사용하면 된다.

<br>

>참고자료 
* You Don't Know JS - 타입과 문법, 스코프와 클로저