---
layout: post
title:  Effective Java Rule.57    
tags: Effective Study 
categories: Effective
---   

이번 Rule은 `예외는 예외적 상황에만 사용하라` 입니다.
Java에서 예외는 다양한 방법/경우에 사용될 수 있습니다. 하지만 이는 잘못된 방식이며, 예외적인 상황에서만 사용해야한다고 말합니다.

#### 잘못된 사용   

책의 예시를 그대로 들고오겠습니다.

    try{
        int i =0;
        while(true){
            rage[i++].climb();
        }
    }catch (ArrayIndexOutOfBoundsException e){
        
    }

> 위 코드보다, 올바른(?) 작성법은 아래와 같습니다.

    for(element e: rage)
        e.climb();
    }

책의 내용으로 돌아와서, 첫번째 코드는 2가지의 측면에서 잘못된 작성 법(?)입니다.
    
    1. 예외처리를 진행하지 않았다.
    2. 예외적 상황에서만 동작하지 않는다.

책에서는 `2`에 초점을 맞춰말하지만, `1`도 생각해볼만한 주제인 것 같습니다.

> 주로 로그를 남기는 방향으로 개발이 진행되는데, 이게 옳은가에 대해서는 토론을 해보죠.

(덧) 예외 블럭의 코드는 최신 JVM이 사용하는 최적화 기법 중, 일부가 적용 안될 수도 있다고 하네요.

#### 예외적 상황에서만 처리를 하라.

위 같은 예외처리를 사용할 경우, 가장 큰 문제는 의도하지 않았던 예외까지도 처리가 된다는 점입니다. 즉, 에러 상황에서 프로그램이 뻗지 않고, 마치 정상적으로 동작하는 것 처럼 보일 수 있습니다.

> 가장 위험한 코드는 예상치 못한 상황에서 정상동작하는 것입니다.

즉, 예외는 예외적 상황에서만 사용해야하며, 평상시 제어 흐름에 이용해서는 안됩니다.

책에서는 조금더 일반화하여 예외뿐만 아니라 코드 작성 시, 쉽게 이해할 수 있는 표준적인 숙어대로 코딩하라고 합니다.

설사 표준적인 숙어보다, 성능이 좋을지라도 플랫폼이 성능이 개선된 미래에도 같은 결과가 나오리라는 확신이 없다면, 사용하지 않는게 좋습니다.
(너무 머리를 많이 굴린 기법일수록 버그 확률은 올라갑니다..)

> 종현님이 떠올랐네요 :D  

또한 이 원칙은 API 설계에서도 적용되는데요.

잘 설계된 API는 클라이언트에게 평상시 제어 흐름의 일부로 예외를 사용하도록 강요해서는 안됩니다.

예를 들어 Iterator을 들 수 있는데요.
(여기부턴 개인적인 해석이 섞여들어갑니다.)

Iterator에는 상태검사 메서드인 `hasNext()` 함수가 존재합니다.

즉, 상태를 검사하는 함수와 가져오는 함수가 별도로 분리되어 있습니다.
사용할 경우 아래 같이 사용할 수 있겠죠.

      List<String> list = Arrays.asList("hello","world");

      Iterator iterator = list.iterator();

      while(iterator.hasNext()){
          System.out.println(iterator.next());
      }

만약 위처럼 검사하는 함수가 없었을 경우, 예외처리를 사용해야합니다.
(다음 element가 있는지 없는지를, 확인 할 수 없기 때문이죠.)


    Iterator iterator = list.iterator();
    try{
        while(condition){
            System.out.println(iterator.next());
        }
    }catch(NoElements ... ){

    }

> API는 클라이언트에게 제어 흐름의 일부로 예외를 사용하도록 강요해선 안된다

위 코드는 클라이언트에게 Exception을 강요하고 있네요.

상태 메서드 외에, 특이값(ex null)을 리턴하도록 설계할 수도 있지만, next()의 결과가 null을 포함 할 수 있기에 위 케이스에 적용하기는 문제가 있습니다.

#### 결론

예외 사용시, 해당 예외가 일반적인 제어 흐름과 연관되어 있는지 확인해야 하며, API뿐만 아니라, 클래스 설계시에도 제어 흐름의 일부로 예외가 사용되지 않도록 신경써야 합니다.

2018.03.22    
lusiue@gmail.com   


