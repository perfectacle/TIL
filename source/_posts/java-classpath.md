---
title: (Java) Classpath
tags:
  - classpath
  - package
  - manifest
date: 2018-09-30 22:59:07
---

현업에서 Spring Boot를 사용하면서 자바/스프링을 제대로 몰라서 기본부터 다져나가야겠다...  
느리더라도 천천히...  
또한 나의 노트 공간이기 때문에 내가 자주 사용하는 Mac OSX 환경을 토대로 설명을 진행하겠다. 

## 기본
아주 기본인 Hello, World부터 찍어보자.  
아무런 IDE도 없이 터미널에서 한다고 가정해보자.  

```bash
cd ~
vim Hello.java
```

그리고 main.java에 **Hello, World!**를 찍어보자.

```java
public class Hello {
    public static void main(String[] args) {
       System.out.println("Hello, world!");
    }
}
```

파일 이름과 메인 메서드를 지닌 클래스의 이름이 일치해야한다.  
Hello.java를 JVM이 이해 가능한 바이트코드(Hello.class)로 컴파일 해보자.  

```bash
javac Hello.java
```

그리고 실제 어플리케이션을 실행해보자.  

```bash
java Hello
# Hello, World!
```

우리가 작성한 어플리케이션이 아주 잘 동작한다.

## Package
> A package is a grouping of related types providing access protection and name space management.
  https://docs.oracle.com/javase/tutorial/java/package/packages.html
  
Package는 관련이 있는(related) Type(classes, interfaces, enumerations, and annotation)들을 모아놓은 것(Grouping)이다.  
관련있는 것들을 모아놔야 높은 응집도(high cohesion)를 만들어서 객체 지향의 원칙 중 하나(응집도는 높이고 결합도는 낮춰라(high cohesion low coupling))를 준수하기 때문이다.  
이렇게 관련 있는 것들을 모아놓으면 Namespace도 만들 수 있어서 다른 패키지의 클래스 이름과도 겹치지 않는다.  
하지만 실제 사용자 관점에서는 동일한 클래스명이 여러 개 있으면 실제 어떤 패키지인지 일일이 확인해봐야하므로 너무 흔하거나 중복된 이름은 피하는 게 좋은 것 같다.  
또한 패키지에 있는 Type들의 접근 지정자(Access modifiers)를 설정할 수 있어서 캡슐화를 도와준다.  

이제는 이 Package라는 걸 이용해서 간단하게 **Hello, World!**를 찍는 어플리케이션을 만들어보자.  

```bash
cd ~
mkdir exam
cd exam
vim Hello2.java
```

이제 Package를 사용해서 어플리케이션을 작성해보자.  
Package와 Directory 명은 일치해야한다.
```java
package exam;

public class Hello2 {
    public static void main(String[] args) {
       System.out.println("Hello, world!");
    }
}
```

이제 JVM에서 실행하기 위해 바이트 코드로 말아보자.  
```bash
javac Hello2.java
```

이제 어플리케이션을 실행해보자.  
```bash
java Hello2
# Error: Could not find or load main class Hello2
# Caused by: java.lang.NoClassDefFoundError: exam/Hello2 (wrong name: Hello2)
```

엥... 분명 현재 디렉토리에 Hello2.java란 파일이 있는데 NoClassDefFoundError가 뜬다.  

> Thrown if the Java Virtual Machine or a ClassLoader instance tries to load in the definition of a class (as part of a normal method call or as part of creating a new instance using the new expression) and no definition of the class could be found.
  The searched-for class definition existed when the currently executing class was compiled, but the definition can no longer be found.
  https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/NoClassDefFoundError.html

뭐 클래스 파일은 있긴 있는데... (즉, 컴파일은 성공했다는 의미이고, 파일의 Location이 틀렸다는 의미도 아님.)  
도대체 뭐가 문제일까...
이를 위한 해결책으로 **Classpath**가 존재한다.

## Classpath
> Classpath is a parameter in the Java Virtual Machine or the Java compiler that specifies the location of user-defined classes and packages.  
  The parameter may be set either on the command-line, or through an environment variable.
  https://en.wikipedia.org/wiki/Classpath_(Java)
  
Classpath는 JVM이나 Java Compiler에서 사용하는 파라미터인데 유저가 정의한 클래스나 패키지의 위치를 명시하는 기능을 한다.  
Classpath는 CLI나 Environment Variable을 통해 설정된다.  

Java Compiler나 JVM은 기본적으로 Environment Variable에 정의된 classpath를 뒤진다.  
없으면 현재 경로(`.`)을 classpath로 설정한다.  
이 포스트에서는 Environment Variable에 classpath가 없다고 가정하겠다.  

그럼 다시 위에서 실행한 명령어를 분석해보자.  
```bash
cd ~/exam
java Hello2
# 아래와 동일하다.
# java -classpath . Hello2
```

그럼 JVM은 이렇게 해석한다.  
1. 현재 디렉토리(`.` -> `~/exam`)에서 Hello2 클래스를 로딩한다.  
2. `package exam;`을 해석해보니 exam 패키지에 있는 녀석이기 때문에 exam 패키지로 이동한다.  
3. exam 패키지가 존재하지 않으니 NoClassDefFoundError가 발생한다.  

3번이 잘 이해가 가지 않는다...  
우리는 분명 exam이란 디렉토리도 만들었으니까 exam 패키지가 존재하는 거 아닌가??  
package는 간단하게 생각해보면 하나의 디렉토리에 불과하다.  
exam 디렉토리 안에서 Hello2 클래스를 로딩했고, 거기에는 exam 패키지(디렉토리)가 존재하지 않는다.  
그렇다면 exam 패키지(디렉토리)가 존재하는 곳은 어딜까?  
바로 Hello2의 바로 상위 디렉토리이다.  
패키지의 시작점(상위 디렉토리)을 Classpath로 지정하면 정확하게 어플리케이션을 실행할 수 있다.  

```bash
cd ~/exam/
java -classpath ../ Hello2
# Error: Could not find or load main class Hello2
# Caused by: java.lang.ClassNotFoundException: Hello2
```

어... 분명 ~/exam 디렉토리에는 Hello2.class가 존재하는데 ClassNotFoundException이 발생했다.  
이름만 봐도 클래스를 찾지 못했다는 예외같다. (즉, 해당 위치에 클래스 파일이 존재하지 않는다는...)  
우리가 classpath를 상위 디렉토리에 지정했으므로 바로 상위 디렉토리에는 Hello2.class가 존재하지 않아서 발생한 예외이다.  
따라서 아래와 같이 실행을 해줘야한다.  

```bash
cd ~/exam/
java -classpath ../ exam/Hello2
# Hello, World!
# 하지만 java에서는 package를 명시할 때 / 대신에 .을 쓰니 아래와 같이 쓰는 걸 권장한다.
# java -classpath ../ exam.Hello2
```

하지만 위와 같이 상위 디렉토리(`..`)으로 classpath를 잡아버리면 `~/exam/`가 아닌 곳에선 무용지물이기 때문에  
상대경로 대신에 **절대경로**를 쓰는 걸 추천한다.  

```bash
cd /
java -classpath ~ exam.Hello2
# Hello, World!
```

`~`를 쓰는 것도 절대경로 같아 보이지만... 사실은 **상대경로**이다.  
`~`는 로그인한 유저의 홈 디렉토리이기 때문에 다른 유저로 로그인 할 때 마다 달라진다.

```bash
# 현재 로그인한 유저의 홈 디렉토리 확인
cd ~
# /Users/yang-gwonseong
pwd

# root 유저로 로그인
sudo su
# root 유저의 홈 디렉토리 확인
cd ~
# /var/root
pwd

java -classpath ~ exam.Hello2
# Error: Could not find or load main class exam.Hello2
# Caused by: java.lang.ClassNotFoundException: exam.Hello2
```

따라서 루트 디렉토리(`/`)로부터 경로를 찾아가는 **절대경로**를 사용해야 해당 커맨드를 모든 유저가 어디서든 사용할 수 있기 때문에 편안해진다.  
```bash
# 현재 로그인한 유저로 어플리케이션을 실행
java -classpath /Users/yang-gwonseong exam.Hello2
# Hello, World!

# root 계정으로 로그인해서 어플리케이션을 실행
sudo su
java -classpath /Users/yang-gwonseong exam.Hello2
# Hello, World!
```

어느 유저로 로그인 했던, 어느 디렉토리에서 접근하던, 절대 경로를 사용하므로 동일한 명령어로 어플리케이션을 실행할 수 있다.
또한 -classpath는 -cp와 같이 줄여서 사용해도 똑같다.

그럼 package를 사용하지 않는 Hello.class의 경우에는 어떨까...

```bash
# Hello.class가 존재하는 디렉토리로 이동
cd ~
java Hello
# Hello, World!

# Hello.class가 존재하지 않는 디렉토리로 이동
cd /
java /Users/yang-gwonseong/Hello
# Error: Could not find or load main class .Users.yang-gwonseong.Hello
# Caused by: java.lang.ClassNotFoundException: /Users/yang-gwonseong/Hello
```
`/`에서는 classpath가 기본적으로 현재 경로(`.` -> `/`)이기 때문에 현재 경로에서는 Hello.class가 없기 때문에 
/Users/yang-gwonseong에 있는 Hello.class를 실행하라고 명령한 것인데 JVM에서는 위 명령어를 다음과 같이 이해한다.  
1. `/`은 패키지 구분자로 이해해서 `(Empty String)` 패키지 안에 `Users` 패키지 안에 `yang-gwonseong` 패키지 안에 `Hello`란 클래스를 찾는다.  
2. 해당 패키지는 존재하지도 않으므로 ClassNotFoundException 발생

Hello.class는 명시적인 패키지가 없으므로(default package를 사용) 아래와 같이 classpath를 입력해줘야 Hello.class가 없는 곳에서도 정상적으로 작동한다.  
```bash
# Hello.class가 존재하지 않는 디렉토리로 이동
cd /
java -classpath /Users/yang-gwonseong Hello
# Hello, World!
```

따라서 어느 유저로 로그인 할지도 모르고... 어디에서 실행할지도 모르므로... 무조건 classpath를 명시적으로 적어줘야 안전하게 어플리케이션을 실행할 수 있다.

## 외부 라이브러리 사용하기
외부 라이브러리를 사용해야할 때도 classpath가 필수이다.  
우선 [Apache Commons Lang](https://commons.apache.org/proper/commons-lang/)을 다운로드 받아보자.  
```bash
cd ~
curl -O http://mirror.apache-kr.org//commons/lang/binaries/commons-lang3-3.8.1-bin.tar.gz
tar xvf commons-lang3-*-bin.tar.gz 
rm -rf commons-lang3-*-bin.tar.gz
```

이제 exam package의 Hello2.java를 Apache Commons Lang을 사용하도록 수정해보자.  
```bash
vim ./exam/Hello2.java
```

```java
package exam;

import org.apache.commons.lang3.StringUtils;

public class Hello2 {
    public static void main(String[] args) {
        System.out.println(StringUtils.defaultIfBlank("    ", "Hello, World!"));
    }
}
```

그리고 평상시와 같이 컴파일을 해보자.  
```bash
javac /Users/yang-gwonseong/exam/Hello2.java
# /Users/yang-gwonseong/exam/Hello2.java:3: error: package org.apache.commons.lang3 does not exist
# import org.apache.commons.lang3.StringUtils;
#                                ^
# /Users/yang-gwonseong/exam/Hello2.java:7: error: cannot find symbol
#         System.out.println(StringUtils.defaultIfBlank("    ", "Hello, World!"));
#                            ^
#   symbol:   variable StringUtils
#   location: class Hello2
# 2 errors
```
1. org.apache.commons.lang3란 패키지를 찾을 수 없다.  
2. StringUtils란 클래스를 찾을 수 없다.  

두 가지 오류가 나오면서 컴파일 에러가 발생했다.  
그럼 Apache Commons Lang의 classpath를 지정해줘서 오류를 해결해보자.  

```bash
javac -classpath /Users/yang-gwonseong/commons-lang3-3.8.1/commons-lang3-3.8.1.jar /Users/yang-gwonseong/exam/Hello2.java
```

오예, 오류 없이 제대로 컴파일 되었다.  

그럼 이제 위 어플리케이션을 한 번 실행해보자!  
```bash
java -classpath /Users/yang-gwonseong exam.Hello2
# Exception in thread "main" java.lang.NoClassDefFoundError: org/apache/commons/lang3/StringUtils
# 	at exam.Hello2.main(Hello2.java:7)
# Caused by: java.lang.ClassNotFoundException: org.apache.commons.lang3.StringUtils
# 	at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:582)
# 	at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:190)
# 	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:499)
# 	... 1 more
```
윽... 실행에 실패했다.  
NoClassDefFoundError가 발생했다...  
`org/apache/commons/lang3/StringUtils`라는 클래스가 정의되지 않았단다...  
클래스로더가 `org.apache.commons.lang3.StringUtils` 클래스를 찾는 것에 실패해서 ClassNotFoundException이 발생하는 바람에 NoClassDefFoundError를 발생시켰다.  
그럼 우린 ClassNotFoundException만 해결하면 된다.  
컴파일 할 때와 마찬가지로 classpath를 지정해주면 된다.  
하지만 우리는 이미 /Users/yang-gwonseong를 classpath로 지정하고 있는데... multiple classpath를 지정하기 위해서는 어떻게 해야할까?  
`:`라는 구분자를 이용해서 multiple classpath를 정할 수 있다.  

```bash
java -classpath /Users/yang-gwonseong:/Users/yang-gwonseong/commons-lang3-3.8.1/commons-lang3-3.8.1.jar exam.Hello2
# Hello, World!
```
우리가 정의한 클래스를 위한 classpath 및 사용한 외부 라이브러리에 대해서도 classpath를 정의해줘야 제대로 어플리케이션을 실행할 수 있다.

## jar 파일로 말아보기
실제로 우리 어플리케이션은 여러 개의 패키지와 클래스로 구성이 될 것이다.  
그렇다면 이걸 배포할 때는 실행 가능한 단일 파일(JAR, Java ARchive)로 만들어야할 것이다.  
이 때 classpath는 어떻게 쓰일까?

좀 더 실용성 있는 예제를 보기 위해 다음과 같은 패키지 구조를 가질 것이다.  
```
+ src
  + com
    + company
      - Adder.java
  + example
    - Hello2.java [Main Class]
```

```bash
cd ~
mkdir src
cd src
mkdir com
mkdir com/company
mkdir example
```

먼저 Util성 클래스인 Adder.java부터 코딩해보자.  
```bash
vim com/company/Adder.java
```
```java
package com.company;

public class Adder {
    public static int add(int x, int y) {
        return x + y;
    }
}
```

그 다음엔 Main 클래스인 Hello2.java를 코딩해보자.  
```bash
vim example/Hello2.java
```
```java
package example;

import com.company.Adder;
import org.apache.commons.lang3.StringUtils;

public class Hello2 {
    public static void main(String[] args) {
        System.out.println(StringUtils.defaultIfBlank("    ", "Hello, World!"));
        System.out.println(Adder.add(1, 2));
    }
}
```

이제 바이트코드로 컴파일하자.  
```bash
javac -classpath /Users/yang-gwonseong/src:/Users/yang-gwonseong/commons-lang3-3.8.1/commons-lang3-3.8.1.jar **/*.java
```
클래스가 여러개(example/Hello2.java, com/company/Adder.java) 일 때 일일이 마는 것 보다 와일드카드 등등의 패턴을 사용해서 한 번에 컴파일하면 편하다.  

이제 메인 클래스를 실행해보자.  
```bash
java -classpath /Users/yang-gwonseong/src:/Users/yang-gwonseong/commons-lang3-3.8.1/commons-lang3-3.8.1.jar example/Hello2
# Hello, World!
# 3
```

우선 jar 파일로 말아보자.  
```bash
cd ~/exam
jar -h
# jar에는 classpath 관련된 파라미터가 없다...
# -c, --create               Create the archive
# -f, --file=FILE            The archive file name. When omitted, either stdin or
#                            stdout is used based on the operation
# -m, --manifest=FILE        Include the manifest information from the given
#                            manifest file
```
따라서 이 때는 Manifest를 만들어야한다!!  

### Manifest
> The manifest is a special file that can contain information about the files packaged in a JAR file.
  By tailoring this "meta" information that the manifest contains, you enable the JAR file to serve a variety of purposes.
  https://docs.oracle.com/javase/tutorial/deployment/jar/manifestindex.html

meta information, information을 위한 정보...  
뭐 jar 파일로 말 때 이 jar에 뭔가 설정을 할 녀석들을 넣어주면 될 것 같다.  
즉 *.jar의 메타 데이터라고 보면 될 것 같다.

```bash
# 디렉토리명은 어디선가 많이 본 이름을 따온 것이므로 그대로 따라갈 필요는 없지만... 자바 개발자 사이의 컨벤션 같으므로 준수하는 게 좋을 것 같다.
mkdir META-INF
# Manifest 파일도 따라갈 필요는 없지만 자바 개발자 사이의 컨벤션 같으므로 준수하는 게 좋아보인다.
vim META-INF/MANIFEST.MF
```

Manifest 내용을 채워주자.

```manifest
Main-Class: example.Hello2
Class-Path: /Users/yang-gwonseong/commons-lang3-3.8.1/commons-lang3-3.8.1.jar
```

다른 설정들도 많지만 우리 클래스를 실행하기 위해 필수적인 설정들만 넣었다.  
Main-Class를 넣지 않으면 `no main manifest attribute, in *.jar`라는 문구와 함께 어플리케이션을 실행할 수 없다.  
또한 외부 라이브러리인 Apache Commons Lang의 classpath도 지정해주어야한다.  
class 파일을 실행할 때와 차이점은 프로젝트의 루트 디렉토리를 클래스패스에 추가해주지 않아도 된다는 점이다.  

이제 jar 파일로 진짜 말아보자.  
```bash
# jar 커맨드는 프로젝트 소스 코드의 루트 디렉토리에서 실행해야한다.
jar -cfm Hello2.jar META-INF/MANIFEST.MF **/*.class
```

-c로 새롭게 생성한다는 걸 알리고,  
-f로 파일명을 정하고
-m으로 Manifest 파일을 지정하고,  
마지막에 메인 클래스 이름을 지정하면 된다.  

이제 실행을 하는데 이 때는 구찮게 classpath를 지정해줄 일도 없다.  

```bash
java -jar Hello2.jar
# Hello, World!
# 3
```

## 마치며
학교에서도 package를 쓰면서 이클립스를 쓰고...
현업에서도 IntelliJ를 쓰다보니 직접 classpath를 지정할 일이 없어서 classpath에 대해서 되게 추상적으로  
클래스의 경로로만 알았는데 명확하게 무엇이며 어떻게 써야하는지...에 대해 좀 알게 된 것 같아  
이제 다른 문서에서 classpath가 나와도 무섭지 않을 것 같다.