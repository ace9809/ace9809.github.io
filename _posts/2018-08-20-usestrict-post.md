---
layout: post
title: 더 좋은 코드를 만들도록! use strict 모드
---

es5에서 엄격모드라는게 새롭게 도입되었다.!!. 이 엄격 모드는 회사 코드에서 처음 접하게 되었는데 익숙해지면 좋은 기능 같아서 글을 쓰게 되었다!
우선 이 엄격 모드는 이름에서 조금 유추할 수 있다 싶이 엄격하게 문법 검사를 해주는 기능이다. 가볍게 이야기를 들자면 선언하지 않고 변수에 값을 정의한다거나
말도 안되던 문법들을 검사해준다.

```javascript
'use strict';
let pirate = 'luffy';
}
```

```javascript
function pirate() {
    'use strict';
    console.log('hi');
}

엄격 모드는 'use strict'라는 키워드로 사용을 할 수 있다. use stirct의 범위는 선언한 scope에 따라 달라지며 전역에 선언을 했을시 전역 컨텍스트에
함수에만 선언을 했을 시 함수안의 context에만 적용이 된다.

<h2>use strict를 왜쓰는가!!?</h2>
자 이제 대충 use strict가 어떤 놈이지 가볍게 알아봤다. 그럼 대체 이녀석은 왜쓰는건지 알아볼 차례이다.
1. 코딩 실수에 대해서 오류를 일으킨다.
2. 자바스크립트에서 안전하지 않은 동작(선언하지 않고 변수에 값을 정의 같은 것들)이 일어날때 오류를 일으킨다.
3. 제대로 고려되지 않은 기능들을 사용할 수 없도록 한다.

<h2>strict mode에서 예외 처리를 일으키는 문법들</h2>

<h4>정의되지 않은 변수 사용</h4>

```javascript
'use strict';
pirate = 'ace'; //Uncaught ReferenceError: pirate is not defined
```
엄격모드에서는 선언 되지 않은 변수를 정의할 수 없다.

<h4>속성 중복</h4>

```javascript
'use strict';
let pirate = {
    ace: 19,
    luffy: 18,
    luffy: 20
}

```

엄격 모드에는 한 속성을 중복해서 정의할 수 없다.

<h4>동일한 매개변수</h2>
```javascript
'use strict';
function pirate(name, name) {
} ///Uncaught SyntaxError: Duplicate parameter name not allowed in this context

```
엄격모드는 동일한 매개변수 이름을 사용할 수 없다.

<h4>8진수 사용</h4>
```javascript
'use strict'
let octal = 010;
let escape = \010;
```
엄격모드에서는 8진수 및 escape문자를 사용할 수 없다.

<h4>엄격모드에서의 this</h4>

```
'use strict';
function pirate() {
    return this;
}
pirate(); //undefined
```
strict모드가 아닐 때 this가 null이나 undefined일 경우 전역 객체로 변환이 되지만 엄격 모드일때는 변환하지 않는다.

<h4>읽기 전용 속성에 값을 할당 할 수 없다</h4>

```javascript
'use strict';
var pirate = Object.defineProperties({}, {
    age: {
        value: 10,
        writable: false // by default
    }
});
pirate.age = 30;
```
<h4>with</h4>

```javascript
with (Math){
    x = cos(3);
}
```
자바스크립트에서 정말 위험한 기능 중 한 개인 with이다. with은 퍼포먼스에 문제가 있어서 흔히 쓰지 말라고 하는데. 엄격모드에서는 with을 사용할 수 없다.

<h4>읽기 전용 속성</h4>

```javascript
'use strict'
var pirate = Object.defineProperties({}, {
    luffy: {
        value: 10,
        writable: false // by default
    }
});
ace.luffy = 19; ///Uncaught TypeError: Cannot assign to read only property 'luffy' of object '#<Object>'
```
Object.defineProperties라는 메서드가 다소 생소할 수도 있을것이다. 이 Object.defineProperties는 객체의 속성을 수정하거나 기존 속성의 특성을 수정하는데
writable을 true로 했을 경우 값을 변경 할 수 있다. 하지만 false로 할 경우 값을 참조만 할 수 있고 변경할 수 없는데. 엄격 모드에서는 writable이
false일 때 값을 변경할 경우 에러를 일으킨다.

<h4>확장 할수 없는 속성</h4>
```javascript
'use strict';
let pirate = {};
Object.preventExtensions(pirate);
pirate.luffy = 19; //Uncaught TypeError: Cannot add property luffy, object is not extensible
```
Object.preventExtensions 메서드는 객체를 확장 불가하도록 만들어준다. 확장 불가하다는 말은 속성을 추가할 수 없다는 말이다. 엄격 모드에서는 확장 할 수 없는
객체에 속성을 추가할 시 에러를 일으킨다.

<h4>delete</h4>
```javascript
'use strict';
let luffy = 19;
function onepiece() {};
let pirate = {};
delete luffy;
delete onepiece;
Object.defineProperty(pirate, 'ace', {
    value: 10,
    configurable: false
    });
delete pirate.ace;
```
엄격 모드에서는 변수, 함수, 매개변수를 기본적으로 삭제할 수 없으며 defineProperty 메서드에서 configurable속성은 해당 객체로부터 속성을 삭제 할 수 있는지 없는지를
설정할 수 있는 속성인데 값이 false인 경우 삭제 할 수 없다.

<h4>예약된 키워드</h4>
implements
interface
package
private
protected
public
static
yield

엄격 모드에서는 위의 키워드를 변수 또는 함수의 이름로 선언할 수 없다.

<h4>eval</h4>
```javascript
'use strict';
let eval = 'hi! i'm eval';  Unexpected eval or arguments in strict mode
```
엄격 모드에서는 eval을 변수나 함수의 이름으로 사용할 수 없다.

```javascript
'use strict';
 eval ("let luffy = 'hi luffy'");
 alert (luffy); //Uncaught ReferenceError: luffy is not defined
```
엄격 모드에서는 eval함수에서 선언된 변수를 외부에서 참조 할 수 없다. 엄격모드가 아닐경우 alert 함수가 정상적으로 실행이 된다.

<h4>arguments</h4>
```javascript
'use strict';
let arguments = 'hi! i'm arguments';  Unexpected eval or arguments in strict mode
```
eval과 마찬가지로 엄격 모드에서 변수나 함수의 이름으로 사용할 수 없다.

```javasciprt
function pirate(name) {
  'use strict';
  name = 'ace';
  console.log(arguments[0]); // luffy
}
pirate('luffy');
```

엄격 모드에서는 파라미터와 arguments의 참조값이 다르다. 엄격 모드가 아닐경우에 name과 arguments[0]의 참조값이 같아 arguments[0]이 ace가 되지만
엄격 모드에서는 파라미터만 바꿨을 경우 arguments의 값은 바뀌지 않는다.