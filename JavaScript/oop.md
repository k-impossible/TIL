## 객체 지향 프로그래밍
객체 지향 프로그래밍(Object Oriented Programming, OOP) 은 기존의 C언어와 같은 절차 지향 언어와는 달리 사람의 생각 방식과 유사한 프로그램 설계 철학이다. 대표적인 객체 지향 언어에는 Java, C#, C++ 등이 있고 자바스크립트는 프로토타입 기반 언어이지만 객체 지향 패턴으로 거의 동일하게 구현할 수 있다. OOP에서는 객체를 데이터와 기능으로 그룹화해서 객체의 재사용성을 높이고 프로그램 유지보수에 용이하다. 

#### OOP의 주요 개념
* __캡슐화 (Encapsulation)__ : 객체의 속성과 메서드를 하나의 단위로 묶어서 객체의 의도를 쉽게 파악하게 할 수 있고 내부 구현이나 데이터는 외부에 드러내지 않아 외부에서 데이터에 직접 접근하는것을 방지하는 은닉화의 특징이 있다.
* __추상화 (Abstarction)__ : 내부 구현과 인터페이스를 분리해 내부 구현은 숨기고 노출되는 인터페이스를 단순하게 만들어서 객체를 사용하는 사람은 인터페이스로만 접근하게해 내부 구현 코드에 영향이 없게 한다.
* __상속 (Inheritance)__ : 부모 객체의 속성과 메서드를 자식 객체가 물려받게 함으로 코드 중복을 줄이고 재사용성을 높인다.
* __다형성 (Polymorphism)__ : 속성과 메서드를 각 객체에 따라 다르게 정의하는 것이다. 오버라이딩으로 부모 객체의 메서드를 자식 객체에서 재정의 할 수 있고 오버로딩으로 객체의 동일한 메서드에 파라미터 개수,자료형을 다르게 해서 다른 동작을 하게 할 수 있다.

<br>

## 클래스와 인스턴스

클래스는 객체의 모델이고 인스턴스는 클래스를 모델로 삼아 만든 하나의 객체이다.
* ES5 클래스 생성
```javascript
function Car(brand, name, color){
	//속성 정의
	this.brand = brand;
  	this.name = name;
  	this.color = color;
}

//메서드 정의
Car.prototype.refuel = function(){ ... }
Car.prototype.drive = function(){ ... }
```
* ES6 클래스 생성
```javascript
class Car{
  //속성 정의
  constructor(brand, name, color){
    this.brand = brand;
    this.name = name;
    this.color = color;
  }
  
  //메서드 정의
  refuel(){ ... }
  drive(){ ... } 	
}
```
* 인스턴스 초기화
```javascript
let avante = new Car("hyundai","아반떼","white");
avante.color; // white
avante.drive(); // 아반떼가 운전을 시작합니다.

let morning = new Car("kia","모닝","black");
morning.brand; // kia
morining.refuel(); // 모닝에 연료를 주입합니다.
```
>* ES6부터는 class	 키워드를 사용해서 클래스를 생성한다. 속성을 정의할 때 constructor를 사용하는데 인스턴스를 초기화할 때 실행되는 생성자 함수이다.
>* new키워드로 인스턴스를 생성할 때 해당 인스턴스가 this의 값이 된다.

<br>

## 자바스크립트 객체 지향의 차이점

#### interface 키워드의 부재
객체 지향 프로그래밍의 주요 개념 중 하나인 추상화를 구현하기 위해 기존 객체 지향 프로그래밍 언어에서는 `interface` 키워드가 제공되지만 자바스크립트에서는 존재하지 않는 기능이다.
* 프로토타입을 이용해 임시 구현
```js
function MotherClass(){
    this.work = function(){
      throw new Error(50, "must override run method");
    }
}
function testClass(){
    this.work = function(){
      console.log("work!");
    }
}

testClass.prototype = new MotherClass();
let test = new testClass();
test.work(); // work!
```
> testClass에서 work메서드가 재정의 되지 않으면 Error:50을 발생시킨다. 프로토타입을 이용하면 간접적인 제약을 줘서 인터페이스 처럼 구현할 수 있다. 

#### private 키워드의 부재
객체 지향 프로그래밍 언어에서는 외부에 노출시키지 않을 속성과 메서드를 구분하기 위해 `private` 키워드가 제공되지만 자바스크립트에서는 해당 키워드가 없다. 자바스크립트에서 은닉화를 하기 위한 일반적인 방법으로 클로저 모듈 패턴을 사용했고 ES2019부터 은닉화를 위한 `#` 키워드를 제공해서 사용 할 수 있다.
* `#` 키워드
```js
class ExampleClass{
  #privateField
  
  #privateMathod(){ ... }
}
```
* 클로저 모듈 패턴
```js
function add(){
  let x = 5;
  
  return function addFive(y){
   	return x + y; 
  }
}

let sum = add();
console.log(sum(6)); //11
```

<br>

>참고자료
* [MDN - OOP](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_programming)
* [MDN - Private class features](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/Private_class_fields)
* [javascript.info - class](https://ko.javascript.info/class)


