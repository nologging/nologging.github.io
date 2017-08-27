---
layout: post
title: 2017년-1학기
tags: review
categories: review
---    


#### 2017 1학기를 마치며.


대학 4년 중, 가장 중요한 내용을 배운 시기가 아닌가 생각하여 간단한 소감을 적어볼까 합니다.     
이번학기는 단순히 수업만 진행한것이 아닌, 개인프로젝트와  any-on이라는 국가프로젝트를 동시에 진행한 학기였습니다. 

#### 함께 일하고싶은 사람.      

면접에서 개발자분이 말씀해주신 내용입니다.     
질문이 자세히는 기억나지 않지만, 기업입장에서 어떤 사람을 뽑을것 같습니까에대한 질문이였습니다. 당시, 어떤 능력을 주로 공부해야할까에 대한 답을 얻고 싶어서 질문을 드렸습니다.    
지금 생각해보면 우문인데, 현답을 주셔서 기억에 남습니다. 	
	
	함께 일하고싶은 사람을 뽑을 것 같습니다.    

이 말을 듣고 한동안 나는 어떤 사람과 일하고 싶을까를 곰곰히 생각해봤습니다. 지금까지 개발을 하면서 많은 사람들과 만나려고 노력했고, 개발자분들의 열정을 닮기위해 노력했던 것 같습니다. 지금까지 만난 개발자분들의 실력또한 부러웠고 닮고싶었지만, 무엇보다 개발에 대한 욕심과 열정이 대단하다는걸 느낄수 있었습니다.     
현업에서 일을 하고 집에 돌아와 개발공부를 하며 개별 프로젝트를 하고, 주말엔 또 다른 개발공부를 하는 분들을 보며 저런 열정을 닮고싶다는 생각을 자주하게 됩니다.  

평소 방에서 Youtube나 보며 쉬던 저였기에, 그분들을 보며 다양한 활동을 하려고 노력했던 것 같습니다.     

제가 함께 일하고 싶은 사람은 개발에 대한 열정과 관심이 있는 사람입니다.     
제가 git 블로그나 개별 프로젝트를 하는 이유 또한, 그분들을 닮고싶어서 진행하는 이유도 있습니다.      

> 공부하는 동기부여가 되기도 하고, 재밌기 때문에 진행하고 있습니다.    
 

 
#### 기억에 남는 수업      

  
이번학기에 가장 기억에 남는 수업은 객체지향언어와 운영체제 입니다.     
객체지향언어는 C++과 JAVA를 이용해 각 언어가 어떻게 객체지향을 구현하는지를 배울 수 있었고, 운영체제는 프로세스/스레드, 교착상태와 병행성에 대해 공부할 수 있었습니다.       

##### 객체지향언어          

JAVA 언어는 어느정도 알고있는 상태였기때문에, 부전공을 위해 학점을 얻을겸, C++도 배워볼겸 수강신청한 과목이였습니다.       

> 사실 .. (속칭) '꿀'같은 과목으로 해당 과목을 수강신청했습니다.      

실제로 꿀을 맛본건 사실이지만... JAVA와 C++에 대해 깊게 생각 할 수 있는 과목이였습니다.

####### C++을 배우며       

그동안 JAVA가 느린 이유에 대해 GC의 존재때문이라고 생각했습니다.      

> 지금 생각해보면 GC때문만은 아니였습니다.    

C++에서 가장 인상깊었던 부분은 생성자 호출시기 그리고 객체 선언에 대한 부분이였습니다.    

객체 선언과 관련하여 JAVA는 객체를 선언할때 new 라는 키워드를 사용하여 Heap 메모리에만 객체를 저장합니다. C++도 new 라는 키워드를 사용할 수 있지만, 객체를 stack영역에 저장하여 사용 할 수도 있습니다. stack영역에 객체를 저장가능하다는 뜻은, Heap 메모리를 할당/해제 할 때의 overhead가 존재하지 않는다는 의미로 해석가능합니다.    
     
> Stack 영역에 객체가 생성된다는 점에서 C++보다 JAVA언어가 overhead가 크다는 점을 알 수 있었습니다.      

이 외에도 앞서 서술한것처럼 GC의 존재도 JAVA의 성능저하를 초래합니다.
GC로 인한  STW(Stop The World)현상이 발생하면서 시스템이 멈추는 현상이 발생합니다. 때문에 실시간으로 통신하는 게임서버는 JAVA언어로 구현을 피한다고합니다.    

> 물론 JVM 버전이 올라가면서, STW현상이 줄어들고 있다고합니다.  
> 무조건 C++보다 JAVA가 느리다고 말할순 없지만, 느릴 수 있는 이유를 공부 할 수 있는 기회가 되었습니다.              


또한 생성자의 호출 시기에 대해 공부할 수 있었는데, 상속관계의 객체간의 부모클래스 생성자가 먼저 호출되고, 자식클래스 생성자가 호출되는 흐름을 배울 수 있었습니다.      
C++에서는 Initialize, JAVA에서는 super()라는 keyword로 특정 생성자를 호출 하여 초기화 한다는 점을 배울 수 있었습니다. 
    

	public static void main(String arg[]){
	    test obj = new test();
	}


	class supers {
	    supers(){
	        System.out.println("super");
	    }
	}
	
	class test extends supers{
	    test(){
	        System.out.println("hello?");
	    }
	}


이와같은 상속 관계에서 test 객체를 생성하면 supers 생성자를 먼저 호출 후, test 생성자를 호출하는 흐름을 볼 수 있습니다. 

	super
	hello?   


해당 수업을 통해서 그동안 몰랐던 부분들을 공부하는 기회가 되었습니다.    



#### OS에 대해      

컴퓨터 공학의 기초 과목이라고 하면, DB, 자료구조 , 알고리즘 , Network , OS 등을 꼽을 수 있습니다.  DB, 자료구조 , 알고리즘은 수강을 했지만, Network , OS를 들을 기회가 없던 중, 이번학기에 시간이 되서 수강 신청을 했습니다.       

어느정도 학교 공부에대해 회의감을 갖고있던 중, OS는 정말 알찬 수업이였습니다.    
프로세스와 스레드, 교착상태와 상호배제, 선점과 비선점, 커널 등  다양한 용어를 배울 수 있었고, 공부할 수 있었습니다. 

> 특히 병행성과 동기화에대해 개념을 정립할 수 있어서 좋은 시간이되었습니다.    


그동안 병행성에 대해 깊게 생각해보지도 않았고 JAVA에서 제공하는 synchronized에 대해서도 '동기화를 제공하나보다' 정도로만 생각하고 있었습니다. OS 수업은 단순히 학점을 따는 목적이 아닌 다른 개발자와 소통할 수 있는 지식을 알려준 수업입니다.     

평소 다양한 개발글들을 보면서 프로세스,스레드등의 단어가 나오면 마우스 휠을 넘기며 다음 글을 읽었고, 자연스럽게 공부할 기회를 잃었다고 생각합니다.       
수업 덕분에 마우스 휠이 넘어가는 빈도가 줄었다고 생각하고, 수업을 마치며 작성할 수 있던 포스팅이 바로 [05-Log4j와System.out.println()](/프로젝트/bookclips/2017/06/25/Log4jandSout/)입니다.     
커널과 동기화에 대한 개념덕분에 코드를 분석하기도 유용했고, 어떤 매커니즘으로 돌아가는지 이해할 수 있었습니다.       

> ( 조금 과장을 더해서 .. ) 대학 4년간 들었던 수업중 가장 알차지 않았나 생각합니다. 



#### 마치며     

대부분의 대학 수업들은 학점을 위한 암기였다고 생각됩니다. 다만, 이번학기에 수강했던 두 과목의 암기는 저에게 충분히 도움이 됬고, 자신감을 준 수업이였습니다.     

의미있는 한학기였기 때문에 짧게나마 글을 작성해 봤습니다.      

   
> 함께 일하고싶은 사람이 되기 위해, 개발에 대한 열정을 보여주려고 노력하고 있습니다.  



lusiue@naver.com     
06-26