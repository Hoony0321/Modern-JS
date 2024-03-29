## 25.1 클래스 프로토타입의 문법적 설탕인가?
---

<br>

JS는 프로토타입 기반 객체지향 언어이다.  
다른 클래스 기반 객체지향 언어와 달리 클래스가 필요없다.  
즉, JS는 클래스가 없어 아래와 같이 객체지향 프로그래밍이 가능하다.  

```javascript
// ES5 생성자 함수
var Person = (function () {
  // 생성자 함수
  function Person(name) {
    this.name = name;
  }

  // 프로토타입 메서드
  Person.prototype.sayHi = function () {
    console.log('Hi! My name is ' + this.name);
  };

  // 생성자 함수 반환
  return Person;
}());

// 인스턴스 생성
var me = new Person('Lee');
me.sayHi(); // Hi! My name is Lee
```

<br>
<br>

* 하지만 클래스 기반 언어에 익숙한 개발자들은 이러한 프로토타입 기반 방식에 혼란을 느낄 수 있다.  
* 따라서 ES6에선 클래스 기반 언어처럼 사용이 가능하도록 **클래스**를 도입했다.
* 실제로는 클래스 모델을 제공하는 것이 아닌 프로토타입 패턴을 클래스 패턴처럼 사용할 수 있도록 하는 **문법적 설탕**이다.


> **Syntactic sugar(문법적 설탕)** : 사람이 이해하기 쉽고 표현하기 쉽게 디자인한 문법

<br>
<br>

클래스는 생성자 함수와 유사하게 동작하지만 다음과 같은 차이점이 존재한다.

<br>

1. 클래스는 new 연산자 없이 호출할 수 없다.
2. 클래스는 상속을 지원하는 extends, super 키워드를 지원한다;.
3. 클래스는 호이스팅이 발생하지 않는 것처럼 동작한다.
4. 클래스 안의 모든 코드는 암묵적으로 strict mode가 적용되어 실행된다. (제거할 수 없다.)
5. 클래스의 constructor, 프로토타입 메서드, 정적 메서드는 모두 [[Enumberable]] 값이 false이다.

<br>
<br>
<br>

## 25.2 클래스 정의
---
class 키워드를 사용하여 정의한다.  
일반적으로 네이밍은 파스칼 케이스를 사용한다.  


 ```javascript
 // 클래스 선언문
class Person {}
 ```

 <br>
 <br>

 일반적이지는 않지만 함수와 마찬가지로 표현식으로 클래스를 정의할 수 있다.
 ```javascript
 // 익명 클래스 표현식
const Person = class {};

// 기명 클래스 표현식
const Person = class MyClass {};
 ```

<br>

 위와 같이 클래스를 표현식으로 정의할 수 있다는 것은 클래스는 일급 객체라는 것을 의미하므로 값처럼 다뤄질 수 있다.

 >ex) 함수의 반환값, 함수의 매개변수로 전달, 자료구조에 저장, 리터럴로 생성


<br>
<br>

클래스 몸체에서 정의할 수 있는 메서드는 **constructor, 프로토타입 메서드, 정적 메서드**이다.

```javascript
// 클래스 선언문
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name; // name 프로퍼티는 public하다.
  }

  // 프로토타입 메서드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }

  // 정적 메서드
  static sayHello() {
    console.log('Hello!');
  }
}

// 인스턴스 생성
const me = new Person('Lee');

// 인스턴스의 프로퍼티 참조
console.log(me.name); // Lee
// 프로토타입 메서드 호출
me.sayHi(); // Hi! My name is Lee
// 정적 메서드 호출
Person.sayHello(); // Hello!
```

<br>
<br>
<br>
<br>

## 25.3 클래스 호이스팅
---

클래스는 함수로 평가된다.
```javascript
// 클래스 선언문
class Person {}

console.log(typeof Person); // function
```

<br>

클래스 선언문으로 정의한 클래스는 함수 선언문과 똑같이 런타임 이전에 평가되어 함수객체를 생성한다.  
이때, 생성자 함수와 프로토타입이 쌍으로 생성된다.  
단, 클래스는 함수 선언문과 달리 정의 이전에 참조할 수 없다는 차이점이 존재한다.  
**즉, 클래스는 호이스팅이 발생하지 않는 것처럼 동작한다.** <br>

```javascript
console.log(Person);
// ReferenceError: Cannot access 'Person' before initialization

// 클래스 선언문
class Person {}
```

<br>

단, 실제로 호이스팅이 발생하지 않는 것은 아니다.

```javascript
const Person = '';

{
  // 호이스팅이 발생하지 않는다면 ''이 출력되어야 한다.
  console.log(Person);
  // ReferenceError: Cannot access 'Person' before initialization

  // 클래스 선언문
  class Person {}
}
```
클래스는 let, const 키워드와 똑같이 선언문 이전에 **일시적 사각지대(TDZ)** 에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작한다.

<br>
<br>
<br>
<br>

## 25.4 인스턴스 생성
---
클래스는 new 연산자와 함께 호출되어 인스턴스를 생성한다.
```javascript
class Person {}

// 인스턴스 생성
const me = new Person();
console.log(me); // Person {}
```

<br>
<br>
<br>

## 25.5 메서드
---
클래스 몸체에는 constructor, 프로토타입 메서드, 정적 메서드 총 3가지 종류의 메서드만 선언이 가능하다.


> **클래스 정의에 대한 새로운 제안 사양**  
> * ES11에 따르면 인스턴스 프로퍼티는 반드시 consturctor 내부에서 정의되어야 한다.
> * 하지만 2021년 1월에 프로퍼티를 constructor 내부가 아닌 몸체에 직접 정의할 수 있는 표준 사양이 제공되었다.
> * 현재 크롬과 같은 모던 브라우저에서는 이미 사용이 가능하다.

<br>
<br>

## 25.5.1 constructor
---
constructor는 인스턴스를 생성하고 초기화하는 특수한 메서드이다. (다른 이름으로 사용할 수 없다.)

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }
}
```


앞에서 말한 것처럼 클래스는 인스턴스를 생성하기 위한 생성자 함수이다.  
그래서 클래스는 평가되어 아래와 같은 함수 객체가 생성된다.  
<br>

<img src="./chap25_1.PNG" width="300px">

<br>
<br>
<br>

### constructor는 생성자 함수와 유사하지만 몇가지 차이점이 있다.

<br>

> **constructor는 클래스 내에 최대 한 개만 존재할 수 있다.**

여러 개의 constructor가 있으면 에러가 발생한다.

```javascript
class Person {
  constructor() {}
  constructor() {}
}
// SyntaxError: A class may only have one constructor
```

<br>
<br>


> **constructor는 생략할 수 있다.**

```javascript
class Person {}
```

<br>
constructor를 생략하면 아래와 같이 암묵적으론 빈 constructor가 정의된다.

```javascript
class Person {
  // constructor를 생략하면 다음과 같이 빈 constructor가 암묵적으로 정의된다.
  constructor() {}
}

// 빈 객체가 생성된다.
const me = new Person();
console.log(me); // Person {}
```

<br>
<br>

> **constructor 매부에서 this를 통해 인스턴스 프로퍼티를 생성할 수 있다.**

```javascript
class Person {
  constructor() {
    // 고정값으로 인스턴스 초기화
    this.name = 'Lee';
    this.address = 'Seoul';
  }
}

// 인스턴스 프로퍼티가 추가된다.
const me = new Person();
console.log(me); // Person {name: "Lee", address: "Seoul"}
```

<br>
이때 초기값을 전달하려면 constructor 매개변수를 선언하고 매개변수로 전달하면 된다.

```javascript
class Person {
  constructor(name, address) {
    // 인수로 인스턴스 초기화
    this.name = name;
    this.address = address;
  }
}

// 인수로 초기값을 전달한다. 초기값은 constructor에 전달된다.
const me = new Person('Lee', 'Seoul');
console.log(me); // Person {name: "Lee", address: "Seoul"}
```

<br>
<br>

> **constructor는 별도의 반환문이 필요없다.**

만약 다른 객체를 명시적으로 반환하면 this가 인스턴스를 가리키지 못하고 명시된 객체를 가리키게 된다.   
즉, 반환된 객체를 생성된 인스턴스로 반환하게 된다.  

```javascript
class Person {
  constructor(name) {
    this.name = name;

    // 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시된다.
    return {};
  }
}

// constructor에서 명시적으로 반환한 빈 객체가 반환된다.
const me = new Person('Lee');
console.log(me); // {}
```

<br>

원시값 반환음 무시하고 this가 반환된다.

```javascript
class Person {
  constructor(name) {
    this.name = name;

    // 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환된다.
    return 100;
  }
}

const me = new Person('Lee');
console.log(me); // Person { name: "Lee" }
```

<br>
<br>
<br>

## 25.5.2 프로토타입 메서드
---

클래스를 이용할 경우 프로토타입 메서드를 정의하기 위해선 다음과 같이 메서드를 추가해야 한다.
```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }

  // 프로토타입 메서드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
}

const me = new Person('Lee');
me.sayHi(); // Hi! My name is Lee
```

<br>
<br>

생성자 함수와 마찬가지로 클래스로 생성한 인스턴스는 프로토타입 체인에 포함이 된다.

```javascript
// me 객체의 프로토타입은 Person.prototype이다.
Object.getPrototypeOf(me) === Person.prototype; // -> true
me instanceof Person; // -> true

// Person.prototype의 프로토타입은 Object.prototype이다.
Object.getPrototypeOf(Person.prototype) === Object.prototype; // -> true
me instanceof Object; // -> true

// me 객체의 constructor는 Person 클래스다.
me.constructor === Person; // -> true
```

<br>

* 즉, 프로토타입 체인은 클래스 생성 방식에도 동일하게 적용된다.
* 이는 결국 클래스도 생성자 함수와 마찬가지로 프로토타입 기반 객체 생성 메커니즘이라는 것이다.

<br>
<br>
<br>

## 25.5.3 정적 메서드
---

정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드를 의미한다.  
메서드에 static 키워드를 붙이면 정적 메서드(클래스 메서드)가 된다.

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }

  // 정적 메서드
  static sayHi() {
    console.log('Hi!');
  }
}
```

<br>
<br>

정적 메서드는 인스턴스로 호출할 수 없다.  
정적 메서드는 클래스에 바인딩이 된다.  
즉, 인스턴스 프로토타입 체인에 클래스 프로토타입은 존재하지만 클래스는 존재하지 않기 때문에 호출이 불가능하다.

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }

  // 정적 메서드
  static sayHi() {
    console.log('Hi!');
  }
}

// 인스턴스 생성
const me = new Person('Lee');
me.sayHi(); // TypeError: me.sayHi is not a function
```

<br>
<br>

## 25.5.4 정적 메서드와 프로토타입 메서드 차이
---
정적 메서드와 프로토타입 메서드는 다음과 같은 차이점이 존재한다.

* 정적 메서드와 프로토타입 메서드가 속해있는 프로토타입 체인은 서로 다르다.
* 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출한다.
* 정적 메서드는 인스턴스 메서드를 참조할 수 없지만 프로토타입 메서드는 가능하다.

<br>
<br>
<br>

## 25.5.5 클래스에서 정의한 메서드의 특징
---

클래스에서 정의한 메서드는 다음과 같은 특징을 갖는다.

* function 키워드를 생략한 메서드 축약 표현을 사용한다.
* 객체 리터럴과 다르게 클래스에 메서드를 정의할 때는 콤마가 필요없다.
* 암묵적으로 strict mode를 사용한다.
* [[Enumerable]] 값이 false이므로  for...in 문이나 Object.keys 메서드로 열거할 수 없다.
* [[Constructor]]를 갖지 않는 non-constructor이다. (new 연산자와 같이 사용할 수 없다.)



