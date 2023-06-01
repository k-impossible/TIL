## 스코프
변수 접근 규칙에 따른 유효범위를 스코프라고 한다.
* 안쪽 스코프에서 바깥쪽 스코프로는 접근이 가능하지만 그 반대로는 불가능
* 스코프는 중첩이 가능
* 가장 바깥의 스코프는 전역 스코프, 그 외 스코프는 지역 스코프
* 지역 변수는 전역 변수보다 우선순위가 높다
```javascript
let globalValue = "Hello World"

function printLog(){
  let localValue = "123"
  globalValue = "Hello JS"
  console.log(globalValue)
}

console.log(globalValue) // "Hello World"
printLog() // "Hello JS"
console.log(globalValue) // "Hello JS"
console.log(localValue) // ReferenceError
```
>* 중괄호로 감싼 범위는 블록 스코프(block scope)
>* 함수로 감싼 범위는 함수 스코프(function scope)
>* 화살표 함수는 블록 스코프에 속한다.

### 변수 선언
ES6부터 javascript에서 변수를 선언하는 방법에 let, const 키워드가 생겼다. 그 이전에는 var 키워드를 썼는데 예측하기 어려운 문제들을 방지하기 위해 쓰지 않는다.
#### let
* 유효범위 : 블록,함수 스코프
* 값 재할당 : 가능
* 재선언 : 불가능 (재선언 시 SyntaxError)
#### const
* 유효범위 : 블록,함수 스코프
* 값 재할당 : 불가능 (재할당 시 TypeError)
* 재선언 : 불가능 (재선언 시 SyntaxError)
#### var
* 유효범위 : 함수 스코프 (화살표 함수의 블록함수는 유효)
* 값 재할당 : 가능
* 재선언 : 가능
#### 변수 선언시 주의점
* var키워드로 변수 선언된 전역 변수 및 함수는 window객체에 속하게 되므로 브라우저의 내장 기능을 사용할때 문제가 발생할 수 있다.
* 전역 변수에 너무 많은 변수를 선언할 시 의도치 않은 문제가 발생할 수 있다.
* var키워드는 블록 스코프를 무시하고 재선언을 해도 에러가 발생하지 않기 때문에 문제를 예측, 발견하기 어렵다.
* 변수 선언 키워드 없이 변수를 선언하면 var로 선언한 전역 변수처럼 된다.
* 여러가지 실수를 방지하기 위해 'use strict'를 사용해 엄격하게 동작하도록 한다.

### 호이스팅

## 클로저
