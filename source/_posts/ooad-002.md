---
title: ooad 002일차
date: 2018-08-01 09:39:57
tags: [OOAD]
---

1일차에 이어서...

## UML vs Thinking in objects
It's useless to learn UML and perhaps a UML Case tool, but not really know how to create an excellent OO design, or evaluate and improve an existing one.
1. It's useless  
여기서 It은 그냥 문장을 시작하기 위한 구조? 란다.  
It's rainy 와 같은 거라고 보면 될 거 같다.  
2. useless to learn UML and perhaps a UML Case tool
UML과 어쩌면 UML case tool을 배우는 것은 쓸모가 없다.  
3. but not really know how to create an excellent OO design  
하지만 훌륭한 OO 디자인을 어떻게 만드는지는 진짜 모른다.  
4. but not really know evaluate and improve an existing one.  
기존 OO 디자인을 개선하고 평가하는 걸 진짜로 모른다.  
여기서 one은 OO design을 의미하는 게 아닐까??

UML과 UML Case tool을 배우는 건 thinking in objects에 비해서 덜 중요하고 덜 쓸모 있지만,(안 중요한 게 아니지만 thinking in objects가 그만큼 중요하다는 뜻?)
좋은 OO design을 하고, 개선하고 평가하는데는 필요할지도 모른다? 필요하다? 이런 뜻인가?? 모르겠당...

It's useless to learn UML and perhaps a UML Case tool, but not really know how to create an excellent OO design, or evaluate and improve an existing one.
얘는 도대체 뭐라고 해석해야할까...;;


Consequently, this book is an introduction to object design
결과적으로 이 책은 객체 설계의 소개이다.  
consequently가 나온걸 보면 이 앞 문장이 object design에 대한 얘기라는 걸 뜻하는 것 같다.  

Yet, we need a language for OOA/D and "software blueprints", both as a tool of thought and as a form of communication
1. Yet, we need a language for OOA/D and "software blueprints"
우리는 ooad와 software blueprints를 위한(에게 적용되는) 언어가 필요하다.  
여기서 language는 programming language가 아니라 communication 수단으로 쓰이는 모든 걸 뜻하는 것 같다.  
일반적으로 communication 할 때 language가 필요하기 때문에 비유적?으로 표현한 것 같다.  
yet? 하지만? 아직은? 아마 하지만인 것 같다.  
앞에서 `programming language가 필요 없다고 thinking in objects가 젤 젤 중요하다`고 얘기 했는데 그래도? 하지만? 여전히? 언어는 필요하다고 한 것 같다.  
2. both as a tool of thought and as a form of communication
생각의 도구와 커뮤니케이션의 형태로써  
아마 both == (as a tool of thought), (as a form of communication)을 의미하는 것 같다.  

Yet, we need a language for OOA/D and "software blueprints", both as a tool of thought and as a form of communication  
하지만 우리는 OOAD와 software blueprints를 위해서 생각의 도구와 커뮤니케이션의 형태가 필요하다.

Therefore, this book explores how to apply the UML in the service of doing OOA/D, and covers frequently used UML.  
1. Therefore, this book explores how to apply the UML in the service  
따라서 이 책에서는 어떻게 서비스에서 UML을 적용하는지 살펴본다.  
앞에서 language가 필요하다, 그건 as a tool of thought and as a form of communication을 위한 거다.  
이런 식으로 설명하고 따라서 그런 language(tool)로써 UML을 쓴다는 뜻 같다.  
2. service of doing OOA/D  
OOA/D의 서비스? OOA/D를 하는 서비스?  
OOA/D로 개발하는 서비스에서 어떻게 UML을 적용하는지 살펴본다는 의미가 아닐까?  
3. Therefore, this book covers frequently used UML.  
따라서 이 책은 자주 사용되는 UML을 다루고 있다.  
cover가 덮다니까 책이 이런 내용으로 덮여있다, 전반적인 내용이 이렇다? 다루고 있다? 로 이해하면 되지 않을까?  
문장도 위와 같이 짤라야하는지 모르지만 일단은 이렇게...  

Therefore, this book explores how to apply the UML in the service of doing OOA/D, and covers frequently used UML.
따라서 이 책은 OOAD를 하는 서비스에서 어떻게 UML을 적용하는지 살펴보고, 자주 사용되는 UML을 다루고 있다.  

## OOD: Principles and Patterns
metaphor: 은유, 비유
certain: 확실한, 틀림없는, 어떤, 무슨 

Also, certain tried-and true solutions to design problems can be (and have been) expressed as best-practice principles, heuristics, or patterns named problem-solution formulas that codify exemplary design principles.
1. Also, certain tried-and-true solutions to design problems  
또한 설계 문제를 해결하는 확실한 tried-and-true 솔루션
tried-and-true solutions는 시도해봤더니 그게 괜찮더라? 문제를 해결해주더라? 참 된 진리더라? 같은 의미를 담고 있는 것 같다.  
직접 시도/경험을 통해서 얻어낸 해결방법을 뜻하는 것 같다.  
2. they can be (and have been) expressed as best-practice principles  
해결법들은 best-practice 원칙으로 표현할 수 있다.(표현된다?)  
best-practice는 모범 사례라고 말할 수 있다.  
they는 앞에 주어, solutions를 뜻하니까 얘는 복수라 they를 썼다.  
3. they can be (and have been) expressed as heuristics
해결법들은 heuristics로 표현할 수 있다.(표현된다?)  
heuristic은 그리스어로 발견하다란 의미를 가지고 있다.  
뭔가를 발견하고 그걸 토대로 학습한다라는 의미를 지니고 있다.  
체험 위주? 뭐 이런 식...
4. they can be (and have been) expressed as patterns  
해결법들은 patterns로 표현할 수 있다.(표현된다?)  
패턴은 특정 규칙을 의미한다.  
5. patterns named problem-solution formulas
문제를 해결 공식이라고 이름지어진? 불리워지는? 패턴들
6. formulas that codify exemplary design principles  
모범적인 디자인 원칙들을 코드화?(코딩?)한 공식들

Also, certain tried-and true solutions to design problems can be (and have been) expressed as best-practice principles, heuristics, or patterns named problem-solution formulas that codify exemplary design principles.
또한 설계 문제를 해결하는 확실한 tried-and-true 솔루션들은 best-practice, heuristics, 모범적인 디자인 원칙들을 코딩한 문제 해결 공식이라고 이름지어진 패턴들로 표현할 수 있다.  

This book, by teaching how to apply patterns or principles, supports quicker learning and skillful use of these fundamental object design idioms.  
1. This book supports quicker learning  
이 책을 빨리 배우는 걸 지원한다.  
2. This book supports skillful  
이 책은 skillful하게 되는 걸 지원한다?  
3. use of these fundamental object design idioms.  
기본적인 객체 설계의 방법들을 사용하여?  
idioms는 관용구, 숙어인데 object design idioms는 object design하는데 자주 쓰이는 것(방법?)들을 의미하는 것 같다.  
여기서 these == fundamental object design idioms, these that fundamental object design idioms이 아닐까?  
4. This book, by teaching how to apply patterns or principles
어떻게 패턴과 원칙을 적용하는지 알려주는 이 책은  

This book, by teaching how to apply patterns or principles, supports quicker learning and skillful use of these fundamental object design idioms.
어떻게 패턴과 원칙을 적용하는지 알려주는 이 책은 객체 설계의 기본적인 방법들을 이용하여 빨리 배우고, skillful하게 되는 걸 도와준다? 지원해준다? 가능하게 해준다?  

## Case Studies
ongoing: 진행 중인
throughout: 전반적인, 내내, ~동안 죽

This introduction to OOA/D is illustrated in some ongoing case studies that are followed throughout the book, going deep enough into the analysis and design so that some of gory details of what must be considered and solve in a realistic problem are considered, and solved.
1. This introduction to OOA/D  
OOAD의 소개  
앞에 This를 붙여서 지금까지 말해온, 지금 말하고 있는 내용/문맥을 의미하는 것 같다.  
2. It is illustrated in some ongoing case studies  
이 소개는 진행 중인 cases study를 뭔가 그림 같은 걸 넣어서 설명한다.  
some이니까 뭐 여러가지 중 대충 몇개 의미하는 거 같다.  
case study는 활용 사례라고 번역되고, 특정 사례(현상)들을 수집해서 집중적으로 탐구하는 걸 뜻한다.  
3. case studies that are followed throughout the book  
책 전반에 걸쳐서 이어지는 case study  
throughout the book 이니까 책 전반에 걸쳐서 나온다는 의미?  
followed 이니까 책 전반에 걸쳐서 뒤따르는? 이어지는?의 의미??  
4. going deep enough into the analysis and design  
이 case study는 분석과 설계에 대해서? 충분히 딥하게 들어간다는 의미같다.  
5. so that some of gory details  
딥하게 들어가서 다루는 내용이 gory details, 유혈 사태를 일으킬 만큼의 디테일?  
그정도로 자세하게 다룬다는 의미를 gory로 비유한 거 아닐까?  
6. gory details of what must be considered and solve
그 gory deatils는 고려돼야만하고, 해결돼야만 하는 것을 의미함.  
7. in a realistic problem are considered, and solved.  
고려돼야하고, 해결돼야하는 현실적인 문제 속에서  

This introduction to OOA/D is illustrated in some ongoing case studies that are followed throughout the book, going deep enough into the analysis and design so that some of gory details of what must be considered and solve in a realistic problem are considered, and solved.
이 OOA/D 소개는 현실적인 문제 속에서 고려돼야하고 해결돼야하는 gory details들을 분석/설계 측면에서 충분히 딥하게 들어가서 책 전반에 걸쳐 진행중인 case study를 그림으로써 설명하고 있다?  
이렇게 설명하면 이상하니까 쪼개서 문장을 이해해야할 거 같다.  
1. 이 책은 진행중인 case study를 책 전반에 걸쳐 다루고 있다.  
2. 이 case study는 분석/설계 측면에서 엄청 딥하게 다루고 있다.  
3. 그 딥한 내용들을 들여다보니 현실적인 문제?(현실 세계) 측면에서도 해결돼야하고 고려돼야하는 문제이다.  

대충 이렇게 이해하면 되지 않을까... 문장 하나가 오지게 길다...  

## Use cases
use case는 UML처럼 일단 다이어그램으로 이해해놓으면 좋다.  
requirements analysis: 요구사항 분석
prerequisite: 전제 조건

OOD(and all software design) is strongly related to the prerequisite activity of requirements analysis, which often includes writing use cases.
1. OOD(and all software design) is strongly related  
객체지향 설계(모든 소프트웨어 설계)는 강하게 연관돼있다.  
2. related to the prerequisite activity  
선행되어야하는 활동과 연관돼있다.  
3. prerequisite activity of requirements analysis  
요구사항 분석의 선행 활동(조건?)  
4. which often includes writing use cases.
OOD는 흔히 use cases를 쓰다? 그리다?도 포함하고 있다.  

OOD(and all software design) is strongly related to the prerequisite activity of requirements analysis, which often includes writing use cases.
OOD는 요구사항 분석 전에 수행해야하고, 흔히 use case를 그리는 것까지 포함하고 있다. 

specifically: 분명히, 명확하게
specify: 명시하다.
specific: 구체적인, 명확한, 특정한 

Therefore, the case study begins with an introduction to these topics, even though they are not specifically object-oriented.  
1. Therefore, the case study begins with an introduction to these topics  
따라서 case study는 use case topic의 소개와 함께 시작한다.  
2. even though they are not specifically object-oriented.  
심지어 걔네들이 객체지향이 아닐지라도...  
case study와 use case가 객체 지향적이지 않다는 의미인가?  
여기서 they가 의미하는 게 무엇일까?  

Therefore, the case study begins with an introduction to these topics, even though they are not specifically object-oriented.
따라서 case study와 use case가 객체 지향적이지 않더라도, case study는 use case topic의 소개와 함께 시작한다.  

## Iterative Development, Agile Modeling, and an Agile UP
Given many possible activities from requirements through to implementation, how should a developer or team proceed?  
1. Given many possible activities  
주어진 많은 가능한 활동들? 이상하다...  
2. activities from requirements through to implementation  
from A to B로 쪼개봐야한다. (A에서 B까지)  
요구사항에서부터 구현하는 활동들  
3. how should a developer or team proceed?  
개발자나 팀은 어떻게 진행해야할까?  

Given many possible activities from requirements through to implementation, how should a developer or team proceed?
요구사항부터 시작해서 구현까지 가는데 다양한 방법들이 존재하는데 개발자와 팀은 어떻게 진행해야할까?  
맞게 번역했는지 모르겠당...;;

Requirements analysis and OOA/D needs to be presented and practiced in the context of some development process.  
1. Requirements analysis and OOA/D needs to be presented and practiced  
요구사항 분석과 OOAD는 나타나져야하고, 연습될 필요가 있다?  
이상하다 정말...  
2. in the context of some development process  
어떤 개발 프로세스의 맥락(문맥)에서?  

Requirements analysis and OOA/D needs to be presented and practiced in the context of some development process.
요구사항 분석과 OOAD는 어떤 개발 프로세스의 맥락에서 보여지고 연습되어질 필요가 있다?  

In this case, an agile(light, flexible) approach to the well-known Unified Process(UP) is used as the sample iterative development process within which these topics are introduced.  
1. In this case, an agile(light, flexible) approach to the well-known Unified Process(UP)  
이러한 경우에 UP라고 알려진 Agile 접근법  
this case는 Requirements analysis and OOA/D 를 뜻하는 게 아닐까?  
agile은 가볍고(무겁지 않다는 것은 실행하는데 오랜 시간이 걸리지 않거나 가볍게 적용할 수 있다는 뜻 아닐까?), 유연하다(다른 애들하고도 잘 어울린다? 애자일을 유동적으로 뭔가 변경할 수 있다?)는 특징을 가지고 있다.  
2. It is used as the sample iterative development process.  
agile approach는 sample iterative development process로써 사양된다.  
sample iterative development process == 반복적인 개발 프로세스 중에 샘플을 의미하는 것 같다.  
3. process within which these topics are introduced.  
이 토픽에서 소개된 프로세스를 의미하는 것 같다.  

In this case, an agile(light, flexible) approach to the well-known Unified Process(UP) is used as the sample iterative development process within which these topics are introduced.
이러한 경우에는 이 토픽에서 소개된 반복적인 개발 프로세스의 샘플로써 잘 알려진 agile UP이 사용된다.  

However, the analysis and design topics that are covered are common to many approaches, and learning them in th context of an agile UP does not invalidate their applicability to other methods, such as Scrum, Feature-Driven Development, Lean Development, Crystal Methods, and so on.

에라 몰라 밥 먹구 출근 ㄲ
