---
layout: post
title: closure 넌 누구냐..?
---

클로저.. 많은 자바스크립트 개발자들이 이름만 알고 실제로 무엇을 하는 기인지 모르고 있는 클로저에 대해서 알아보도록 하겠다!!
일단 클로저를 한 마디로 정의 하자면 내부함수가 외부 함수의 스코프에 접근 할 수 있다. 라고 일단은 이해하면 좋을 것 같다. 함수 안에 함수를 정의한다.
클로저를 한 번도 접하지 못한 개발자는 무슨말인지 이해 못 할 수도 있을 것이다. 일단 코드를 보자!
```javascript
function pirate(name) {
    let content = `${name} is pirate!`
    return function() {
        return content;
    }
}
```
위의 코드는 과연 클로저일까? 아닐까? 정답은 클로저가 아니다.
단순히 함수안에 함수를 정의하는 것이 클로저라고 오해하고 있는 사람들이 있는데 그건 클로저에 대한 오해이다.
pirate 라는 함수 scope안에 익명함수와 content변수가 있기 때문에 익명함수에서 content를 참조 할 수 있다. 이건 그냥 단순히
자바스크립트 scope에 대한 예제라고 보는게 더 맞을 것 같다. 예제 한 개를 더 보도록 하자 !
```javascript
function pirate(name) {
    let content = `${name} is pirate!`
    return function() {
        return content;
    }
}

let onepiece = pirate('ace');
onepiece(); // ace is pirate!
```
앞서 만들었던 함수를 그대로 onepiece 변수에 담아서 호출을 했더니 `ace is pirate`라는 결과값이 나왔다.
혹시 눈치 챘을지도 모르겠지만. pirate라는 함수는 익명함수를 return하고 함수 실행이 끝나서 실행 컨텍스트에서 사라졌을 것이다.
onepiece 함수를 실행시켰을시 여전히 외부함수를 참조하고 있다. 그렇다!! 이것이 클로저의 매커니즘이다.
내부 함수가 외부 함수를 어떻게 참조할 수 있는지 설명을 하자면 //여기도 공부
