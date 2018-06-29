---
title: (Java) FlatMap으로 요소 무시하기
date: 2018-06-29 01:33:27
tags: [Java, Stream]
---
기본적으로 map은 요소를 무시하지 못하기 때문에 조건에 맞지 않는 애들은 아래와 같이 필터링 해줘야한다.  
```java
public class Ttest {
    @Test
    public void test() {
        List<Integer> numbers = Lists.newArrayList(1, 2, 3, 4);

        List<String> strings = numbers.stream()
                                      .map(integer -> (integer % 2 == 0) ? integer + "" : null)
                                      .filter(Objects::nonNull)
                                      .collect(toList());

        assertThat(strings.size(), is(2));
        assertThat(strings.get(0), is("2"));
        assertThat(strings.get(1), is("4"));
    }
}
```

하지만 flatMap을 쓰면 null을 리턴하지 않고, filter를 태우지 않고도 원하는 결과를 만들 수 있다.
```java
public class Ttest {
    @Test
    public void test() {
        List<Integer> numbers = Lists.newArrayList(1, 2, 3, 4);

        List<String> strings = numbers.stream()
                                      .flatMap(integer -> (integer % 2 == 0) ? Stream.of(integer + "") : Stream.empty())
                                      .collect(toList());

        assertThat(strings.size(), is(2));
        assertThat(strings.get(0), is("2"));
        assertThat(strings.get(1), is("4"));
    }
}
```
