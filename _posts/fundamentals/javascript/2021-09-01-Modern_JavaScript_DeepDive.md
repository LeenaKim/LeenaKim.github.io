---
the valayout: post
title: <deepDive> [10] 모던 자바스크립트 Deep Dive
subtitle : 모던 자바스크립트 Deep Dive 10
tags: [javascript, book]
author: Leena Kim
comments : true
---

![cover](/assets/img/post_img/Modern_js_Deep_Dive/modern_js_deep_dive_book_cover.png)



< 모던 자바스크립트 Deep Dive 10장 >



# 객체 리터럴

## 객체란?

원시 타입은 단 하나의 값만 나타내지만 객체 타입은 다양한 타입의 값을 하나의 단위로 구성한 복합적인 자료구조이다. 또한 원시 타입의 값, 즉 원시 값은 변경 불가능한 값이지만 객체 타입의 값, 즉 객체는 변경 가능한 값이다. 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키와 값으로 구성된다. 

```javascript
var person = {
  name: 'Lee', // name : 프로퍼티 키 / lee : 프로퍼티 값
  age: 20
};
```

<br>

자바스크립트의 함수는 일급 객체이므로 값으로 취급할 수 있다. 따라서 함수도 프로퍼티 값으로 사용할 수 있다. 프로퍼티 값이 함수일 경우, 일반 함수와 구분하기 위해 메서드라 부른다.

```javascript
var counter = {
  num: 0,
  increase: function() { //메서드
    this.num++;
  }
};
```

<br>

<br>

## 객체 리터럴에 의한 객체 생성

클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다. 자바스크립트는 프로토타입 기반 객체지향 언어로서 클래스 기반 객체지향 언어와는 달리 다양한 객체 생성 방법을 지원한다.

- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

객체 리터럴은 객체를 생성하기 위한 표기법이다. 객체 리터럴은 중괄호({...}) 내에 0개 이상의 프로퍼티를 정의한다. 변수에 할당되는 시점에 자바스크립트 엔진은 객체 리터럴을 해석해 객체를 생성한다.

```javascript
var person = {
  name: 'Lee',
  sayHello: function() {
    console.log(`Hello! My name is ${this.name}.`);
  }
}
console.log(typeof person); // object
console.log(person); // {name: "Lee", sayHello: f}
```

객체 리터럴은 자바스크립트의 유연함과 강력함을 대표하는 객체 생성 방식이다. 객체를 생성하기 위해 클래스를 먼저 정의하고 new 연산자와 함께 생성자를 호출할 필요가 없다. 숫자 값이나 문자열을 만드는 것과 유사하게 리터럴로 객체를 생성한다. 객체 생성 이후에 프로퍼티를 동적으로 추가할 수도 있다. 객체 리터럴 외의 객체 생성 방식은 모두 함수를 이용해 객체를 생성한다.

<br>

<br>

## 프로퍼티

객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다. 프로퍼티를 나열할 때는 쉼표로 구분한다. 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야 한다. 

```javascript
var person = {
  firstName: 'Ung-mo',
  'last-name': 'Lee'
};
```

<br>

문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 이 경우에는 프로퍼티 키로 사용할 표현식을 대괄호([...])로 묶어야 한다.

```javascript
var obj = {};
var key = 'hello';

// ES5: 프로퍼티 키 동적 생성
obj[key] = 'world';
// ES6: 계산된 프로퍼티 이름
// var obj = { [key]: 'world'};
```

<br>

프로퍼티 키에 문자열, 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다. 

```javascript
var foo = {
  0: 1,
  1: 2,
  2: 3
};
console.log(foo); // {0: 1, 1: 2, 2: 3}
```

<br>

이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다. 에러는 발생되지 않는다.

```javascript
var foo = {
  name: 'Lee',
  name: 'Kim'
};
console.log(foo); // {name: "Kim"}
```

<br>

<br>

## 메서드

프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라 부른다. 후에 더 자세히 배울것이다.

```javascript
var circle = {
  radius: 5,
  
  getDiameter: function() {
    return 2 * this.radius;
  }
};

console.log(circle.getDiameter());
```



<br>

<br>

## 프로퍼티 접근

- 마침표 프로퍼티 접근 연산자(.)를 사용하는 **마침표 표기법**
- 대괄호 프로퍼티 접근 연산자([...])를 사용하는 **대괄호 표기법**

대괄호 표기법 사용의 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다. 

```javascript
var person = {
  name: 'Lee'
};
console.log(person.name);
console.log(person['name']);
```

<br>

프로퍼티 키가 식별자 네이밍 규칙을 준수하지 않는 이름이라면 반드시 대괄호 표기법을 이용해야 한다. 

```javascript
var person = {
  'last-name': 'Lee',
  1: 10
};

person.'last-name'; // SyntaxError
person.last-name; // NaN

person[last-name]; // referenceError
person['last-name']; // Lee

person.1;	// syntaxError
person.'1'; // syntaxError
person[1]; // 10
person['1']; // 10
```

**여기서 문제!**

예제중 person.last-name 의 실행 결과는 Node.js 환경에선 ReferenceError: name is not defined 이고, 브라우저 환경에서는 NaN이다. 왜일까?

> 자바스크립트 엔진은 먼저 person.last를 평가하는데, last 가 키인 프로퍼티가 없기 때문에 person.last는 undefined로 평가된다. 따라서 person.last-name은 undefined-name 과 같다. 다음으로 자바스크립트 엔진은 name이라는 식별자(프로퍼티 키 아님)를 찾는다. 
>
> Node.js 환경에서는 현재 어디에서도 name이라는 식별자 선언이 없으므로 ReferenceError: name is not defined라는 에러가 발생한다. 그런데 브라우저 환경에서는 name이라는 전역변수(전역 객체 window의 프로퍼티)가 암묵적으로 존재한다. 전역 변수 name은 창(window)의 이름을 가리키며, 기본값은 빈 문자열이다. 따라서 person.last-name은 undefined - '' 와 같으므로 산술 계산을 할 수 없다는 뜻인 NaN이 나오게 된다. 

<br>

<br>

## 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

```javascript
var person = {
  name: 'Lee'
};

person.age = 20;
```



 <br>

<br>

## 프로퍼티 삭제

`Delete` 연산자는 객체의 프로퍼티를 삭제한다. 이때 `delete` 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다. 

```javascript
var person = {
  name: 'Lee'
};

person.age = 20;
delete person.age;
delete person.address; // address 프로퍼티가 존재하지 않음. 에러는 발생하지 않음. 
```

<br>

<br>

## ES6에서 추가된 객체 리터럴의 확장 기능

### 프로퍼티 축약 표현

ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략할 수 있다. 이때 프로퍼티 키는 변수 이름으로 자동 생성된다.

```javascript
let x = 1, y = 2;

const obj = { x, y };
```

<br>

### 계산된 프로퍼티 이름

문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 단, 표현식을 대괄호로 묶어야한다. 이를 계산된 프로퍼티 이름이라 한다.

ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

```javascript
const prefix = 'prop';
let i = 0;

const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i
};
console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

<br>

### 메서드 축약 표현

ES5에서는 메서드 정의시 프로퍼티 값으로 함수를 할당한다. ES6에서는 메서드를 정의할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.

```javascript
const obj = {
  name: 'Lee', 
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi();
```

ES6의 메서트 축약 표현으로 정의한 메서드는 프로퍼티에 할당한 함수와 다르게 동작한다. 후에 자세히 배워보자. 

