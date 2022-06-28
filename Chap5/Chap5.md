## 5.1 값
---
값은 식이 평가되어 생성된 결과를 말한다.
변수는 하나의 값을 저장한 메모리 공간을 식별하기 위해 붙인 이름을 말한다.

## 5.2 리터럴
---
러터럴은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법을 말한다.

> [...] -> 배열 리터럴<br>
> function(){...} -> 함수 리터럴<br>
> { 'key' : 'value' } -> 객체 리터럴<br>
> '문자열' -> 문자열 리터럴<br>
> true & false -> 불리언 리터럴 <br>
> etc...<br>

## 5.3 표현식
---
표현식은 값으로 평가될 수 있는 문(statement)이다.
```javascript
// 리터럴 표현식
10
'Hello'

// 식별자 표현식(선언이 이미 존재한다고 가정)
sum
person.name
arr[1]

// 연산자 표현식
10 + 20
sum = 10
sum !== 10

// 함수/메서드 호출 표현식(선언이 이미 존재한다고 가정)
square()
person.getName()
```

## 5.4 문(statement)
---
문(statement) & 표현식(expression)이라는 용어가 자주 등장할텐데, 둘을 헷갈리면 안된다.<br>

>statement는 프로그램을 구성하는 기본 단위이며 최소 실행 단위이다.<br>
>expression은 값으로 평가될 수 있는 statement의 특별한 경우이다.<br>

<br>

statement는 token으로 이루어진다.<br>
token이란 문법적인 의미를 가지며, 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소를 의미한다.

> ex) var sum = 1 + 2; <br>
> token = [ var , sum , = , 1 , + , 2 , ; ] <br>

## 5.5 세미콜론과 세미콜론 자동 삽입 기능
---
세미콜론은 statement의 종료를 나타낸다.<br>
즉, JS엔진은 세미콜론을 통해 statement의 끝을 파악하고 순차적으로 다음 statement를 실행한다.<br>
따라서 statement 끝날 때마다 세미콜론을 붙여야 한다.<br>

<br>

>JS엔진에서 자동으로 statement의 끝이라고 예측되는 지점에 세미콜론을 자동 삽입해주기 때문에 생략이 가능한 경우도 존재한다.


## 5.6 표현식인 문과 표현식이 아닌 문
---
```javascript
// 변수 선언문은 값으로 평가될 수 없으므로 표현식이 아니다.
var x;
// 1, 2, 1 + 2, x = 1 + 2는 모두 표현식이다.
// x = 1 + 2는 표현식이면서 완전한 문이기도 하다.
x = 1 + 2;
```
statement중에 expression인 것과 아닌 것을 구별하기 어려울 수 있다.<br>
이럴 땐, 변수에 할당해보면 명확히 구분이 가능하다.<br>
expression은 값으로 평가되기 때문에 변수에 할당하는 것이 자연스러우면 expression이고 아니면 표현식이 아닌 statement이다.<br>



