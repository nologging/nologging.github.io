---
layout: post
title:  You don't know Js-typeof-instanceOf
tags: JS
categories: Book
---

이번장에서는 `typeof` 와 `instanceOf`에 대해 설명합니다.


#### Prototype

	var wrapperNum = new Number(5);
	wrapperNum._proto_  // 출력으로 prototype을 볼 수 있습니다.

prototype을 이용해서 OOP의 상속구조처럼 프로그램을 설계할 수 있는데,
예를 들면 Array의 prototype을 들고 있는 경우, 기본적으로 제공하는 `join()`,`push()`,`map()`등의 함수를 사용할 수 있습니다.

native 함수를 통해 생성된 객체 뿐아니라, `new` keyword를 이용해 생성된 객체는 `_proto_` 속성을 지닙니다.

#### 예시

	function TestPrototype(){
		this.value = 5;
	}
	// convention :: new를 이용하는 함수는 첫 문자를 대문자로 사용합니다.  
	var testPrototypeObj = new TestPrototype();
	TestPrototype.prototype.add = function(addValue) { this.value += addValue};

	testPrototypeObj.add(3); // 8

위와같은 방식으로 prototype를 정의(함수 및 변수)할 수 있습니다.


> prototype에 대한 깊은 설명은 여기선 하지 않겠습니다.
> 추후 기회가 된다면 별도의 포스트로 진행하겠습니다.


#### typeOf and instanceOf

책에서 나오지 않은, prototype을 설명한 이유는 instanceOf를 설명하기 위해서 입니다.

typeOf와 instanceOf는 비슷한듯 하지만 전혀다른 방식으로 동작합니다.

	typeOf value // value의 type을 알려주며, Wrapper 된 객체의 경우 "object"를 반환합니다.

> 예시

	typeof new String() // "object"
	typeof "name" // "string"
	function testFunc(){}
	typeof new testFunc // "object"
	typeof testFunc // "function"

> 주의 typeof new Function 의 반환값은 "function" 입니다

(개인적으로 이해한 부분은) prototype을 갖고있으면 object, 갖지않으면 알맞은 "[type]"을 반환한다. 로 생각하고 있습니다.
요 부분은 검색을해보니 `type tag` 라는 값으로 판단을 하는듯 한데, 꽤나 이해하기 어려워 설명하지 않겠습니다.

> 정확하지가 않아서요 ..

#### Function has not prototype

Native인 Function은 사실 prototype을 갖고 있지 않습니다.
`new Funtion()`으로 생성된 변수를 출력해보면 분명 `_proto_`를 들고 있는걸 볼 수 있지만, spec에 호환되기 위해 생성된 부분이며 proto 에 정의된 함수는 모두 undefined를 반환합니다.

> 즉, 이전엔 없었다가 스펙 호환을 위해 생긴듯합니다.
> 때문에 undefined를 반환하긴 하지만, prototype 속성을 갖고 있어  instanceOf Function 로 사용될 수 있습니다.


[참조](http://www.ecma-international.org/ecma-262/6.0/#sec-properties-of-the-function-prototype-object)

#### InstanceOf

InstanceOf는 변수가 같은 prototype 들고있으면 `true` , 아니면 `false`를 반환합니다.

	var str = new String();
	str instanceOf String // true
	str instanceOf Object // true
	// prototype chaining 으로 Object를 가르키고있습니다.

	var fun  = new Function();
	fun instanceOf Function // true

	function name() {};
	name instanceOf Function // true
	new name() instanceOf Function // false
	// new 를 선언하는 순간 자신만의 prototype을 갖습니다.

> TODO typeof 내부 로직 파악

#### typeof 의 오류

> Null 에 관하여

typeOf와 null을 함께 사용하면 예상치 못한 결과값을 뱉습니다.

	typeof null // "object"

js를 잘 모른 상태에서 위 코드를 보게된다면,

	"js는 null도 object구나!!"

라고 생각하게 될지도 모릅니다.  ~~잘못된 생각입니다.~~

위는 명백히 틀린 결과값입니다.  
js를 설계할 당시 버그가 있었고, 발견된 시점에선 이미 많은 곳에서 코드가 사용되고 있어 수정할 수 없었다고 합니다.

> 하위호환성을 위하여 ...

그러니 다른 언어에서처럼

	var str = null;

변수를 `null`로 초기화하는 것은 지양해야합니다.


#### 마치며

원래는 ydk-js 3장에 함께 설명하려했으나, 정리하면 할 수록 책의 내용과는 동떨어져서 별도의 포스트로 분리했습니다.

아직 미숙한 부분이 많습니다.
읽어주셔서 감사합니다.

lusiue@gmail.com  
2018.08.25  
