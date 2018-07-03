---
title: Lombok @Builder
date: 2018-07-04 02:03:33
tags: [Java, Lombok]
---

롬복에서 아주 유용한 어노테이션이 @Builder이다.  
클래스와 생성을 분리(? 맞나?) 시켜주는 패턴인 빌더 패턴을 구현할 때 유용하다.  
클래스를 내/외부로 빼내지 않아도 되고, 그냥저냥 쓸만하게 잘 뽑아주는 것 같다.  

```java
@Builder
public class VO {
    private long id;
    private String pw;
}
```

하지만 위와 같이 하면 기본 생성자는 날아간다.  
따라서 기본 생성자를 쓰려면 아래와 같이 @NoArgsConstructor를 추가해줘야한다.  
```java
@Builder
@NoArgsConstructor
public class VO {
    private long id;
    private String pw;
}
```

하지만 모든 필드를 가지고 있는 생성자를 제외한 생성자를 가지고 있는 경우에는 아래와 같이 오류가 난다.  
`Error:(6, 1) java: no suitable constructor found for VO(long,java.lang.String)`
```java
@Builder
@NoArgsConstructor
public class VO {
    private long id;
    private String pw;

    public VO(long id) {
        this.id = id;
    }
}
```

따라서 아래와 같이 @AllArgsConstructor를 추가해줘야한다.  
```java
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class VO {
    private long id;
    private String pw;

    public VO(long id) {
        this.id = id;
    }
}
```

그리고 필드에 기본값을 넣고 싶다면 아래와 같이 필드 위에 @Builder.Default 어노테이션을 추가해줘야한다.  
```java
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class VO {
    private long id;

    @Builder.Default
    private String pw ="pw";

    public VO(long id) {
        this.id = id;
    }
}
```

기본적인 사용 방법은 아래와 같다.  
getter는 알아서 추가하자.  
```java
public class VOTest {
    @Test
    public void test() {
        VO.VOBuilder builder = VO.builder();

        VO vo = builder.id(1).build();
        assertThat(vo.getId(), is(1L));
        assertThat(vo.getPw(), is("pw"));

        VO vo2 = builder.id(2).pw("aa").build();
        assertThat(vo2.getId(), is(2L));
        assertThat(vo2.getPw(), is("aa"));
    }
}
```

플러그인도 뭔가 귀찮았던 거 같은데 잘 된 거 같다.  
아주 간편하다.