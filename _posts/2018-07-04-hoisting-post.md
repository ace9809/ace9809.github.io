---
layout: post
title: Hoisting 이란?
---

<h2>what is hoisting?</h2>

자바스크립트를 개발하다보면 호이스팅이라는 개념을 한 번쯤은 들어봤을 것이다. 호이스팅은 변수와 함수 선언을 맨 위로 이동시키는 행위를 하는 자바스크립트 매커니즘이다.
```bash
console.log(pirate); // undefined
var pirate = 'luffy';
console.log(pirate); // luffy
```
위 코드의 결과를 보고 호이스팅을 공부하기전에 난 "왜 pirate 변수를 선언하지도 않았는데 첫 번째 콘솔에서 undefined가 뜬 것이지? ReferenceError: pirate is not defined 가 떠야 정상 아닌가?" 라는 의문점이 들었었다.
지금 위의 코드는 우리가 배울 호이스팅이 일어난 것이다.
아까 우리는 호이스팅이 변수와 함수 선언을 맨 위로 이동시킨다고 배웠다. pirate 변수를 정의 하는 코드가 최상단으로 올라갔기 때문에 변수를 선언하지도 않았는데도 오류가 나지 않고 pirate 값이 undefined가 뜨게 된 것이다.
호이스팅이 일어난 위의 코드를 다시 정의 하면 밑에와 같다.
```bash
var pirate;
console.log(pirate); // undefined
pirate = 'luffy';
console.log(pirate); // luffy
```
함수일 경우에도 호이스팅이 되지만 함수 선언문만 호이스팅이 되고 함수 표현식은 되지 않는다.
```bash
///함수 선언문
ace(); //fire fist
function ace() {
    console.log('fire fist');
}
```

```bash
///함수 표현식
var ace = function() {
    console.log('fire fist');
}
```

변수명과 함수명이 같고 호이스트가 될 때 함수 선언은 변수 선언보다 우선순위가 높다.
```bash
var pirate;
function pirate() {
    console.log(hello);
}
console.log(typeof pirate); //function
```

변수의 값이 있을때는 변수 선언이 함수 선언보다 우선 순위가 높다.

```bash
var pirate = 'luffy';
function pirate() {
    console.log(hello);
}
console.log(typeof pirate); //string
```bash

```bash
var pirate = 'luffy';
function pirate() {
    console.log(pirate); /// undefined
    pirate = 'zoro';
    console.log(pirate); /// zoro
}
```

```bash
var pirate = 'luffy';
function strawHat() {
    var pirate = 'zoro';
    console.log(pirate);
}
```bash

console.log의 출력값은 zoro가 나온다. 왜 첫 번째라인에 코드에서 전역 변수를 선언 했음에도 불구하고 출력값이 zoro가 나오는 이유는 자바스크립트는 function scope이기 때문이다.
코드를 보면 전역변수로 pirate의 값을 luffy로 주고 함수안에 pirate라는 변수를 또 정의했다.  이는 전역변수인 pirate와는 다른 strawHat의 지역변수를 새롭게 만든 것이기 때문에
이름은 같지만 엄연히 서로 다른 변수이기 때문에 출력값이 zoro가 나온다.

<h2>strict mode</h2>
엄격 모드에서는 선언하지 않은 변수를 사용할 경우 에러가 난다.
```bash
'use strict';
console.log(number);
var number = 4; //Uncaught ReferenceError: number is not defined
```
<h2>es6</h2>
```bash
console.log(fruit); // Uncaught ReferenceError: fruit is not defined ...
let fruit = 'apple';
console.log(age); // Uncaught ReferenceError: age is not defined ...
const age = 17;
```
let과 const는 var과 다르게 호이스팅이 되지 않는다.
자바스크립트에서 var로 변수를 선언하는 경우는 변수를 선언함과 동시에 초기화가 동시에 진행되고 변수에 값을 할당하는 과정을 거친다.   그래서 우리가 앞선 호이스팅 예제에서 초기화가 이루어졌기 때문에 undefined 값이 나온 것이다.
하지만 let과 const의 경우는 선언과 초기화가 동시에 진행이 되지 않는다.  초기화는 변수 선언문이 정의 되었을때 실행이 되는데 초기화가 되기전에 TDZ(Temporal Dead Zone)에 들어가게 된다.  위의 코드처럼 변수 선언문이 정의되지 않았는데 참조를 할 경우
tdz단계이기 때문에 ReferenceError가 뜨게 되는 것이다.
*다른 블로그를 보면 let과 consts는 호이스팅이 되지만 tdz에 빠져서 ReferenceError가 뜬다는 글이 많은데 만약 호이스팅이 된다면 위의 코드에서 let fruit;가 위에 선언이 된다는 이야기일텐데 이는 이미 초기화가 된 상태이므로 undefined가 떠야 정상일 것이다. 하지만 그렇지 않기 때문에 let과 const는 hoisting이 된다고 볼 수 없다고 생각한다*

참조
*https://scotch.io/tutorials/understanding-hoisting-in-javascript