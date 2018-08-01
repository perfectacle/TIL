---
title: ooad 001일차
date: 2018-07-30 22:35:00
tags: [OOAD]
---
OOAD 책을 보면서 글로 끄적여야 좀 머리에 남는 것 같아...
하루하루 깨작깨작 대보자...

# Object Oriented Analysis and Design
Time is a great teacher,
시간은 훌륭한 선생이다. 
but unfortunately it kills all its pupils
하지만 불행하게도 시간은 모든 학생을 죽인다?  

좋은 선생(학습법?)이 그의 학생들(제자들)을 모두 죽인다, 안 좋은 결과를 초래할 수도 있다는 얘기인 것 같다.  
시간은 좋으면서도 안 좋은, 장점과 단점(장점을 덮어버릴 만큼의)이 존재한다는 얘기 같다.

Describe - 묘사하다 기술하다 말하다   
Illustrate - 삽화(그림?)를 쓰다(넣다, 이용하다), (뭔가 예를 들어서) 보여주다

Describe는 글(text, 말)로써 설명하는 느낌이고 Illustrate는 그림(글보다 더 시각화된 자료)으로써 설명하는 느낌이다.  

Objective는 목적,목표


## What will you learn? Is it useful?

what does it mean to have a good object design?  
1. what does it mean
무슨 의미인가
2. which to have a good object to design?  
좋은 객체 설계를 가진다는 것

it == which to have a good object to design
좋은 객체 설계를 가진다는 것은 무슨 의미인가? 어떤 의미인가?

core - 핵심, (과일의) 속, 중심부

essential - 필수적인, 중요한
robust - 팔팔한, 튼튼한, 견고한
maintainable - 유지보수성? 유지보수 가능한?

Core skills in OOAD(object oriented analysis design) skills are essential for the creation of well-designed, robust, and maintainable software using OO technologies and languages such as Java or C#
1. Core skills in OOAD(object oriented analysis design) are essential
OOAD의 핵심 스킬들은 필수적이다.
2. essential for the creation of well-designed software
잘 설계된 소프트웨어를 만드는데 필수적이다.  
essential for the creation of robust software  
견고한 소프트웨어를 만드는데 필수적이다.    
essential for the creation of maintainable software  
유지보수 가능한 소프트웨어를 만드는데 필수적이다.  
3. software using OO technologies
객체 지향 기술들을 사용한 소프트웨어  
software using OO languages as Java or C#.  
자바나 씨샵 같은 객체지향 언어를 사용한 소프트웨어

OOAD의 핵심 스킬들은 잘 설계되고, 견고하고, 유지보수 가능한, 객체 지향 기술들과 자바나 씨샵 같은 객체지향 언어를 사용한 소프트웨어를 만드는데 필수적이다.  

evolutionary - 진화의, 점진적인  
shape - 모양으로 만들다. 형상화하다. 형성하다. 
be presented - 나타나다. 보여지다.

iterative and evolutionary development shapes how ooad is presented in this book.  
1. iterative and evolutionary development shapes   
반복적이고 점진적인 개발은 형상화한다.
2. how ooad is presented
어떻게 ooad가 보여지는지
3. in this book  
이 책에서  

반복적이고 점진적인 개발은 이 책에서 ooad를 어떻게 보여주는지 형성하고 있다?(이상하다...)  

evolve - 발달하다(시키다), 진화하다(시키다)
across - 건너서/가로질러
case study - 사례 연구(굳이 해석하지 말자...), 하나 또는 몇 개의 사례를 중심으로 분석하는 연구, 특정 사례를 들어 학습하는 방법인 것 같다.

the case studies are evolved across three iterations
1. the case studies are evolved
케이스 스터디는 발전되어왔다?(진화됐다?)  
2. across three(iterative, evolutionary, agile) iterations
세 가지를 반복함으로써

케이스 스터디는 세 가지(iterative, evolutionary, agile)을 반복함으로써 발전해왔다.  

proverb - 속담

owning a hammer doesn't make one an architect
1. owning a hammer
해머를 가지는 것(건축가에게 필요한 장비)  
2. it doesn't make one
해머를 가지는 것은 한 사람을 만들지 않는다.  
3. one an architect
한 사람을 한 명의 아키텍트(건축가)로

망치를 가지고 있다고 해서 건축가가 되지 않는다.  

respect to - ~에 대한

the proverb is especially true with respect to object technology
1. the proverb is especially true
이 속담은 참 트루(리얼)이다.  
2. with respect to object technology
오브젝트 기술에 대해서

이 속담은 객체 기술에 대해서 사실이다. 꼭 맞음!

sufficient - 충분한
self-sufficient - 자급자족 할 수 있는
insufficient - 불충분한

knowing an object-oriented language(such as Java) is a necessary but insufficient first step to create object systems.
1. Knowing an object-oriented language(such as java) is a necessary
자바와 같은 객체 지향 언어를 아는 것은 필수적이다.
2. but insufficient first step
첫 단계로는 충분하지 않다.  
3. to create object systems.  
객체 시스템을 만드는데  

자바와 같은 객체 지향 언어를 아는 것은 필수적이지만, 객체 시스템은 만드는 첫 단계로는 충분하지 않다.  
객체 시스템을 만들기 위해서 분석/설계/구현 등등이 있는데 객체 지향 언어로 할 수 있는 건 구현인데 객체 시스템을 만들 때는 구현이 제일 먼저(첫 단계)는 아니란 소리 같다.  

critical - 핵심적인, 비판적인  

**Knowing how to "think in objects" is critical**
객체 내에서 사고하는 방법을 아는 게 핵심적이다!

this is an introduction to ooad while applying the unified modeling language and patterns.  
1. this is an introduction to ooad
이것은 ooad의 소개다.  
2. while applying the unified modeling language and patterns
uml과 pattern을 적용하는 것에 대한
while이 ~에 대한으로 쓰였다.   

이것은 ooad의 소개인데 그 소개의 내용은 uml과 pattern을 적용하는 것까지이다?
이것은 ooad의 소개인데 그 소개의 내용은 uml과 pattern을 적용하는 것까지 포함한다?

And, to iterative development, using an agile approach to the Unified Process as an example iterative process
1. And, to iterative development
그리고 반복적인 개발
2. And, using an agile approach
그리고 에자일 접근법을 사용하여
3. to the Unified Process
통일된 프로세스 
4. as an example iterative process
as an example == iterative process??
as an example that iterative process??
반복 프로세스의 예로

그리고 반복적인 프로세스의 예로 반복적인 개발, 애자인 접근법을 사용한 통일된 프로세스

아래와 같이도 쪼개질 것 같다.  
1. to iterative development as an example iterative process
2. using an agile approach to the Unified Process as an example iterative process

그리고 바로 위에 적어놓은 문장하고도 이어지는 것 같은데 길어서 쪼갠 것 같다.  
this is an introduction to ooad while (applying the unified modeling language and patterns) and (to iterative development, using an agile approach to the Unified Process as an example iterative process)

mastery - 숙달, 통달  
frequently - 자주, 흔히  

(applying the unified modeling language and patterns) and (to iterative development, using an agile approach to the Unified Process as an example iterative process)
emphasizes mastery of the fundamentals, such as how to assign responsibilities to objects, frequently used UML notation, and common design patterns
1. it emphasizes
저런 놈들은 강조한다.  
2. mastery of the fundamentals
기초 지식(근본적인 걸 숙달 하면 기초 지식이 되는 듯...?)  
3. such as how to assign responsibilities to objects.
어떻게 객체에게 책임을 할당하는지(단일 책임 원칙과도 연관이 있는 듯 !)  
4. frequently used UML notation,
주로 UML 표기법을 사용하여   
5. frequently used common design patterns
주로 공통적인 디자인 패턴을 사용하여

저런 놈들은 주로 UML 표기법과 디자인 패턴을 사용하여 어떻게 객체에게 책임을 할당하는 지와 같은 기초 지식을 강조한다.  

mostly in later chapters, the material progresses to some intermediate-level topics such as framework design and architectural analysis.
1. mostly in later chapters  
대부분 챕터(챕터 1, 2, 3...)의 마지막 부분에는
2. the material progresses  
the material == later chapters
대부분 챕터의 마지막 부분에는 진행한다.  
3. to some intermediate-level topics  
중급 주제  
4. such as framework design and architectural analysis  
프레임워크 설계와 아키텍처스러운(?) 분석

대부분 챕터의 마지막 부분에는 프레임워크 설계와 아키텍쳐 분석과 같은 중급 주제를 진행한다.  

## UML vs Thinking in objects
The book is not just about UML.
이 책은 단지 UML에 관한 책이 아니다.  
UML 전문 서적이 아니고 UML을 딥하게 다루는 서적도 아니고 단순히 UML을 커뮤니케이션 도구로만 사용한다는 의미인 듯...?  

Common notation is useful, but there are more important OO things to learn especially, how to think in objects.
1. Common notation is useful  
Common notation = UML diagram
일반적인 표기법은 유용하다  
2. but there are more important OO things
OO와 관련된 거에는 Common notation보다 훨씬 중요한 게 있다.  
3. OO things to learn especially
OO와 관련된 배울 것
4. how to think in objects  
어떻게 객체 중심의 사고를 할 것인가  

일반적인 표기법은 유용하지만 그것보다 훨씬 중요한 어떻게 객체 중심의 사고를 할 것인가와 같이 OO 관련해서 배울 것들이 있다.  
UML 같은 표기법 보다 객체 중심 사고가 훨씬 중요하다는 사실을 나타내는 구문 같다.

The UML is not OOA/D or a method, it is just diagramming notation.
UML은 OOAD나 어떠한 수단이 아니고 단지 다이어그램 표기법이다.  
UML이 뭐 만능 킹왕짱은 아니란 소리인 듯... 글케 크게 중요하지도 않고 단순 표기법에 불과하다는 사실...  

It's useless to learn UML and perhaps a UML Case tool, but not really know how to create an excellent OO design, or evaluate and improve an existing one.
1. It's useless  
여기서 It은 how to think in objects를 뜻하는 것 같다.  
객체 중심의 사고를 하는 건 쓸모 없다.  
2. to learn UML and perhaps a UML Case tool
UML을 배우는 것, 어쩌면 UML Case tool을 배우는 것까지도


consequently - 그 결과, 따라서

에라 몰라 자자...
