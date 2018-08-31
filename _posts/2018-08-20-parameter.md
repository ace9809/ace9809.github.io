---
layout: post
title: 매개변
---


<h2>매개변수</h2>

javascript에서 함수의 매개변수는 기본적으로 undefined 입니다

```javascript
functionName(parameter1,parameter2,parameter3){
	code to be executed
}
```

함수 매개변수(parameters)는 함주 정의에 나열한 names입니다

함수 인수(arguments)는 함수에 전달된 실제 값(values)입니다

자바스크립트 인수(arguments)는 값(value)로 전달됩니다

함수는 값(value)만 알고 인수(arguments)는 모른다

함수로 인수의 값을 변경하면, 매개 변수의 원래 값은 변경되지 않습니다

인자없이 함수가 호출되었을 경우, 빠진 인자 값들은 undifined로 설정 된다

```javascript
function findMax() {
		var i, max = 0;
		for(i = 0; i < arguments.length; i++){
			if(arguments[i] > max){
				max = arguments[i];
			}
		}
		return max;
	}
	findMax(1,5,7); // 7
```

함수는 인자 객체에 의해 호출되는 내장된 객체이다

인자 객체는 함수가 호출될 때, 사용될 인자 값들의 배열을 포함한다