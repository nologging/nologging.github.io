---
layout: post
title:  Effective-Java
tags: Study 
categories: Java
---   

이번 포스트에서는, Annotation과 관련된 2가지 규칙을 설명합니다. 

    @Override 어노테이션은 일관되게 사용하라
    자료형을 정의할 때 표식 인터페이스를 사용하라 

#### @Override  

@Override 는 상속 및 구현시, `함수의 재구현`을 의미하는 Annotation입니다.
책에서는 Annotation을 일관되게 사용해야하며, 그랬을 때의 장점들을 나열하고 있습니다.

#### 함수의 오타 및 잘못된 구현을 막을 수 있다.  

만약 사용자가 equals()라는 함수를 구현한다고 가정해봅시다. 
@Override를 사용하지 않을 경우 아래와 같이 사용해도 컴파일 에러는 나타나지 않습니다.

    public void equals(){ ~ }

예상했던 Object의 equals가 아니라 새로운 equals함수가 만들어 졌고, 컴파일러는 똑똑하지 않기에(?) 이를 에러로 취급하지 않습니다.

> 언젠가 그런 컴파일러가 나오길 바랍니다 .. 

#### 추상클래스 / 인터페이스의 경우 모두 붙여라   

일반적으로 추상클래스 -> 클래스 / 인터페이스 -> 클래스 의 관계에서는 @Override를 붙이지 않아도 컴파일단에서 에러를 뱉기에 큰 문제는 없습니다. (구현이 강제되기 때문이죠.)

다만 `추상클래스 -> 추상클래스`  및 `Interface -> 추상 or 인터페이스`의 관계에서는 @Override를 붙이라고 말합니다. 
그 이유는 만약 override를 붙이지않고 오타를 내거나, 잘못된 시그니쳐를 사용할 경우 컴파일러는 에러를 내지 않으며, 명시적으로 상위 클래스의 메서드와 하위클래스에서 생성된 메서드를 구별하기 위함입니다.

대표적인 예시로, Collection 과 Set 관계가 그렇다고 하네요 :D

#### 자료형을 정의 할 때 표식 인터페이스를 사용하라 

`Rule.37은 자료형을 정의할 때 표식 인터페이스를 사용하라`라는 Rule 입니다.

표식인터페이스(Marker Interface)는 아무 메서드도 선언하지 않은 인터페이스를 의미합니다. 예전 Rule에서 봤던 Serializable 이 여기에 해당합니다.

Annotation을 공부하면서 이런 생각을 했었습니다.

>  아무런 메서드도 선언하지 않은 Interface를 사용할 바엔, Annotation을 쓰면 되는거 아냐 ?

바로 이 질문에 대한 답을 이번 Rule에서 보여줍니다.  

#### Marker Interface / Marker Annotation  

Marker Interface의 장점은 아래와 같습니다.

    1. 자료형이다.
    2. 적용범위를 세밀하게 정할 수 있다.

> 자료형이다. 

(책 자체를 이해하기는 어려움을 겪어, 개인적인 추측을 섞었습니다. )

OOP에서 상속/구현은 확장에 대해 다룸니다. 만약 annotation을 사용할 경우, 협력관계의 재사용은 불가피해지며, 이는 결국 확장에는 닫혀있는 코드가 될거라 예상합니다.
때문에 자료형이다. 라는 첫번째 장점은 OOP적인 특성을 말하는게 아닐까요 ...?
(조심스레 추측해봅시다. - 도와줘요 )

> 적용범위를 세밀하게 정할 수 있다.

(이건 어느정도 테스트를 해봐야할 거같은데 .. )

클래스 계층 구조에서 Interface를 추가하면 하위 로직에 모두 적용되지만, annotation은 그게 아니라고 이해했습니다. 
(이건 토의를 해봐야할거 같아요 ... 테스트도 .. 해볼게요 )

#### 정리하며  

자료형이 필요하다면 인터페이스를 쓰고, 그 외의 프로그램적 요소를 다룰 때는 Annotation을 쓰세요 ! 

> 조금 더 생각이 필요할거 같네요 ...


    
