---
layout: post
title:  HighPerformance-Web-1
tags: HighPerformance-Web WEB
categories: book-webPerformance
---   

   
#### High Performance WEB    

#### Rule.1 HTTP 요청을 줄여라.

어찌보면 당연한 Rule인데, 책에서는 어떻게 HTTP 요청을 줄이는지 서술한다.  

꽤 다양한 방법들이 있었는데, 크게 공감하지 못했던 부분들도 많아서 그 부분들은 한줄로 요약했다.

	1. 여러개의 img를 연속적으로 보여줘야할 때, img Map 을 사용한다. 
	2. 연속되지 않은 img인 경우, Css sprite를 사용하여 요청을 줄일 수 있다. 
	3. Data Schema 사용 

CSS Sprite는 여러 이미지를 하나로 합친 후 좌표값을 이용해 특정 Img를 사용하는 방식으로 사용 할 수 있다.
이렇게 사용하면 Request 한번에 모든 Img를 가져오는 것과 유사해진다. 
(다만 사용하기는 조금 까다로울 거 같다.)

> 위 세가지 방법들은 '써봐야겠다!' 라기보다 '쓸수 있을까?' 라는 생각이 먼저 들었다 ..  


또 한가지 방안은 Gulp.js 등을 이용한 스크립트 통합(?)이다. 여러 js 파일들을 하나로 합쳐 관리하는 것으로 1번의 요청으로 필요한 js를 가져올 수 있다.

주로 기능별로 모듈화한 js 파일을 필요에따라 통합하고, minify 하는 절차를 거친다. 

> '사용해 보면 좋겠다.' 라는 생각을 할 수 있었다.  

다만 여기서 고민해봐야할 부분은 "특정 페이지에 어떤 모듈들을 합칠 것인가?"에 대한 문제이다.
이부분은 Cache를 언급할 때, 함께 정리할 예정이다. 

Rule.1은 "이렇게 해야된다 !" 라는 느낌보다 "이런게 있다 ?" 라는 느낌을 받았다 ..  



#### Rule.2 콘텐츠 전송 네트워크를 사용하라 .

콘텐츠 전송 네트워크 (CDN) ... 

개인적으로 CDN은 jquery나, Handlebars등의 js 파일들을 다운받기 위해 사용했었다. 사실 파일을 다운받아 로컬서버에 두고, 그걸 참조하도록 적는게 ~~귀찮아서~~ 사용했던건데 책에서는 조금 다르게 사용하더라 ...  

기본적으로 "로딩속도에 영향을 끼치는 것에 무엇이 있는가 ?" 라고 생각해보면 컨텐츠 크기, 대역폭, 네트워크 속도 등을 생각할 수 있는데 책에서 CDN 을 사용하는 이유를 "위치"라고 말한다. 

즉, Client와 Server간의 거리가 속도에 영향을 주기에 사용자 근처에있는 CDN을 사용하면 `구성요소`들의 속도를 빠르게 만들 수 있고 결과적으로 로딩시간을 단축 시킬 수 있다. 

> 실제 사용자의 서버를 분산시키지 않는 이유는, 로드밸런싱 , 세션동기화 , replaction.. 등이 있다...  

다만 CDN 또한 서버이기 떄문에 여러 서버가 하나의 cdn을 바라볼 경우, 응답속도가 떨어진다.

또한 CDN을 사용하면 실제 서버는 `구성요소` 들 외에 데이터를 전달하는데에만 집중할 수 있다는 이점이 존재한다. 


이렇게 빠르면 HTML 도 CDN에 두면 되지않나 ? 라는 생각을 할 수 있는데, 보통 그러진 않는다.
HTML은 단순한 정적 페이지가 아닌지라, DB 및 Compile등의 과정을 거쳐야하기떄문이다.   

> 즉, 정적 파일만 CDN에 넣어야한다.   



Rule.1 , Rule.2 는 그냥 맛보기 느낌 ...
