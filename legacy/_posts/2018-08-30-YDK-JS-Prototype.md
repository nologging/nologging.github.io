---
layout: post
title:  You don't know Js-prototype
tags: JS
categories: Book
---


#### Prototype

Js에서는 Prototype 이라는 기능을 통해 OOP의 상속과 유사한 기능을 수행할 수 있습니다.
이번 장에서는 Prototype에 대한 전반적인 개념을 정리했습니다.


#### new function  

대표적인 OOP 언어인 JAVA / C++ 에서는 `new Class` 형태로 object를 생성합니다.
하지만 js는 class라는 개념을 갖고있진 않습니다,(es6에서 생깁니다.)
그래서인지.. 조금 생소하게도, new keyword를 function과 함께 사용할 수 있습니다.

```
  function People(name, age){
    this.name = name;
    this.age = age;
  }

  var people = new People("chulwoon", 25);
  console.dir(people);
```

this의 개념을 알고있는 사람이라면, 위 코드가 이렇게 동작한다고 생각하겠죠 .. (?)

  1. 함수 호출시, `bind()`를 사용하지 않았으므로, this는 window가 될것이다.
  2. `return` 코드가 없으므로 undefined를 반환할 것이다.

예상과는 다르게도 위 코드는 `Pople` 객체를 반환합니다. 여기서부턴 위 함수를 `생성자 함수`라고 부르도록 하겠습니다.


> 여담으로  ..

함수를 설계시, `생성자 함수인가/ 일반 함수 인가?` 에 따라 내부 구현이 달라질 수 있습니다. (this)
때문에 일반적인 convention으로 생성자 함수일때, class처럼 첫 글자를 대문자로 사용합니다.


#### new / non-new

`new`를 사용하여 생성된 함수와 일반 함수는 몇가지 차이점을 갖고 있습니다.
저는 `this`,`return this`, `prototype` 3가지 관점(?)에서 정리하도록 하겠습니다.

#### this

위 예시를 다시 가져와봅시다.

```
  #case using new
  function People(name, age){
    this.name = name;
    this.age = age;
  }

  var people = new People("chulwoon", 25);
  console.dir(people);
```

여기서 한줄만 추가하면 큰 차이(?)를 알 수 있습니다.

```
  # case no using new
  var generalPoeple = People("chulwoon",25);
  console.log(generalPoeple);
```

큰 차이는 `this`가 전역이 아니라는 점 입니다.
new를 사용하여 함수를 생성할 경우, this는 함수 자기 자신이 됩니다. 때문에 `#case using new`에서의 this는 People 함수가 되어 자신의 scope에 변수를 할당합니다.

> 1. new 를 사용할 경우 this는 함수 자기 자신이다.

또한 new를 사용할 경우, 함수의 결과 값은 자기 자신(`this`)입니다.

  var people = new People("chulwoon", 25);

때문에 `People`함수에 `return` 코드가 없어도 `var people`에 결과값이 저장됩니다.

#### prototype  

console에 `var people`을 찍어보면 `__proto__`라는 새로운(?) 인자를 확인할 수 있습니다.


> new / non-new 의 가장 큰 차이는 요 부분입니다.

`__proto__`은 prototype이라는 의미로, 같은 함수로 생성된 Object들은 같은 Prototype을 가르킵니다.
가장 기본적으로(?) 함수의 공통된 값을 저장할때 prototype을 사용할 수 있습니다.  

> `__proto__`는 prototype을 가르키는 Link 입니다.

```
  function Pc(){
    this.price = 95;
    this.model = "Samsung"
  }

  var model1 = new Pc();
  var model2 = new Pc();
```


만약 위처럼 함수마다 `공통된` 값을 들고있을 경우 위 코드를 이렇게 바꿀 수 있습니다.

```
  Pc.prototype.model = "Samsung";
  function Pc(){
    this.price = 95;
  }

  var model1 = new Pc();
  var model2 = new Pc();

  model1.model; // Samsung
  model2.model; // Samsung
```

`this.model`을 선언하지 않았음에도 `Samsung`이 출력되는 이유는 scope chaining 때문입니다.
변수 참조시, 지역변수가 없으면 전역변수를 바라보듯이, 객체 또한 변수가 할당되어 있지 않으면 `__proto__` 속성을 타고 들어가 해당 변수를 찾습니다.

변수 뿐만 아니라, prototype을 이용해 함수를 저장할 수도 있습니다.

> js는 function이 first citizen  이니까요.


  Pc.prototype.add = function() {this.price += 10;}
  model1.add(); // price가 105가 됩니다.

이러한 Prototype을 이용해서 Array / String / Boolean 등의 Native 객체들이 기본 함수를 제공합니다.

> String.split, Array.join 등이 prototype에 정의되어 있습니다.

#### Warning

Prototype은 꽤나 매력적이지만, 몇가지 주의해야할 점이 있습니다.


#### 변경시 주의

prototype은 같은 함수로 생성된 객체들이 공통으로 바라보는 공간입니다.
때문에 prototype이 변경 될 경우, 하위 모든 타입들에게 영향을 줄 수 있습니다.

> 게다가 prototype chaining을 이용한 상속구조(?) 일 경우 영향받은 객체가 많이질 수있습니다.

#### + prototype chaining

Prototype을 이용하면 Java의 상속구조와 비슷한 구조를 사용할 수 있습니다.

```
  function Mechanic(){
    this.type = "Mechanic";
  }

  Pc.prototype = new Mechanic();
```

위 처럼 사용할 경우, Pc의 prototype이 Mechanic(this)가 되고 Prototype chaining이 일어나게 됩니다.

> 만약 pc 의 prototype에 값이 없다면 Mechanic 까지 올라가서 변수를 찾습니다.

이렇게 chaining 할 경우, Java의 상속과 비슷한 느낌으로 개발을 할 수 있으나, 과도한 chaining의 경우 결국 불필요한 비용이 들 수 있습니다. (성능 저하..)



#### 마치며


간단하게 prototype을 정리해봤습니다.
js에서 prototype을 이용해서 개발할 일은 거의 없겠지만, 이미 구현된 시스템을 이해하는데는 꼭 필요한 지식입니다.

읽어주셔서 감사합니다 :D

lusiue@gmail.com
