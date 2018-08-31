---
layout: post
title: 생성자의 대해서 공부해 보즈아!
---

객체를 만드는 방법은 여러가지가 있을 것이다. 보통은 객체 리터럴과 생성자 함수를 이용해서 만드는 경우가 많으니 이 두 경우에 대해서 공부하도록 하자. (프로토 타입을 이용해서도 인스턴스 객체를 만들 수 있으나 워낙 내용이 방대하니 따로 정리를 해놓았다. 여기)
```javascript
let ace = {
    age: 21,
    fruit: fire
}
```
우리는 객체를 지금 한 ace라는 객체를 객체리터럴 방식으로 만들었다. 그런데 여기서 또 프로퍼티가 같은 luffy라는 객체를 만들려면 똑같이 ace객체를 만들었던 것 처럼
만들어줘야 한다. 만들어야 할 객체가 많지 않으면 상관이 없겠지만 밀짚보자 해적단의 객체를 만든다고 가정했을때 똑같은 코드를 9개나 작성해야 하는 것이다.
상당히 비효율적이지 않은가!!!? 나 같이 귀찮음이 많은 프로그래머는 한 줄이라도 코드를 더 줄이고 싶은데 말이다. 그러기 위해서 있는게 바로 생성자 함수다.
생성자 함수는 이름에서 조금? 유추해 볼 수 있듯이 객체를 만들어주는 함수이다. 함수가 어떻게 객체를 만들어주지?라고 생각할 수도 있다. 하지만 지금부터 어떻게
만들 수 있는지 자세히 알아보도록 하자
*es6에선 드디어 클래스가 추가되었다.!! 클래스에 대해선 따로 정리할 것이니 참고하길 바란다.

<h2>생성자 함수</h2>
아까 우리가 만들었던 객체를 능력자들의 정보를 만들어주는 생성자 함수로 간단하게 표현하면 아래와 같다.
```javascript
function Pirate(age, fruit) {
    this.age = age,
    this.fruit = fruit
}

let ace = new Pirate(21, 'fire');
let robin = new Pirate(22, 'flower');
```

생성자 함수를 Pirate를 사용하여 ace와 robin 두 개의 객체를 만들었다. 이 때 생성자 함수를 통해 만들어진 객체를 인스턴스라고 한다.
자 이제! 생성자 함수가 어떻게 생긴 놈인지 알았으니 어떻게 해서 객체가 만들어 지는건지 공부를 해 보자.
일단은 생성자 함수의 이름은 첫 글자는 대문자로 짓는다. 소문자로 해도 상관은 없지만 일종의 컨벤션이라고 생각하면 좋을 것 같다.
함수를 호출할때 new를 붙여주면 함수를 객체로 만들어 준다.
```javasciprt
function test() {}
console.log(test();
console.log(new test());
```
위의 예제에서 new를 붙여서 호출한 콘솔은 객체를 반환하는걸 볼 수 있다. 우리는 new를 붙여서 Pirate 생성자 함수를 만든 것이며 쉽게 말하면 객체를 만들었다고 생각하면 된다.
함수에서는 아무 것도 return을 하지 않을시에 undefined를 리턴하지만 생성자 함수는 this를 자동으로 리턴한다. 만약 우리가 생성자 함수를 호출한 뒤 인자값을 아무것도 넣지 않는다면
age와 fruit의 값이 undefined인 객체를 반환 할 것이다. 생성자 함수에서는 this키워드를 가지고 property를 추가 할 수 있다.

<h2>new를 넣지 않는 경우</h2>
여기까지 글을 읽었으면 한 가지 호기심이 들 것이다. 그럼 new를 안넣으면 어떻게 될 까??
```javascript
function Pirate(age, fruit) {
    this.age = age,
    this.fruit = fruit
}

let ace = Pirate(21, 'fire');
let robin = Pirate(22, 'flower');
```
앞에서 공부했던 예제와 똑같은 코드지만 new를 뺐다. 과연 이 코드는 어떻게 실행이 될 까? 앞에서 new 키워드는 객체 만들어주는 키워드라고 설명을 했다.
그런데 new를 빼고 Pirate만 호출했을 시 이 Pirate는 객체가 아닌 그냥 함수일 뿐이다. 함수에서 this는 window객체를 바라보고 있고 우리는
window객체에 age와 fruit라는 property를 생성하게 된 것이다.

