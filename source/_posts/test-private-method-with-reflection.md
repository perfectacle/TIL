---
title: Private Method 테스트하기
date: 2018-07-06 01:49:29
tags: [Test, Java, JUnit, Reflection]
---

private 메소드는 기본적으로 외부 클래스에서 접근이 불가능해서  
테스트 클래스에서 접근하려면 default 메소드로 빼지 않는 이상은 불가능하다.  

진짜 private을 유지하면서 테스트 하려면 reflection을 이용하는 수 밖에 없다.  
하지만 reflection을 사용하면 메서드 이름을 **String**으로 넘겨야해서 IDE가 제대로 replace를 해주지 않는다면 낭패를 볼 것이다.  
하지만 테스트가 깨지는 일은 매우 자주 있는 일이며, 리팩토링 하면 재사용 불가능한 테스트 코드가 되어버리기도 해서  
어차피 깨질 테스트 코드에 그렇게 안정성에 의미를 둘 필요는 없는 것 같다.  

누군가는 프라이빗 메서드는 테스트하지 마라, 프라이빗 메서드를 테스트하려는 욕구가 든다면 그건 이미 설계 자체가 잘못 된 것이다.  
라고 얘기 하는데... 나는 아직 아키텍트가 아닌가보다 ㅠㅠ  
퍼블릭을 테스트 하려면 너무 덩치가 큰 녀석을 테스트 해야하는 사태가 발생하기도 하궁...
에라 모르겠당 나는 프라이빗을 테스트 해서 좀 더 작은 단위로 테스트 하고 싶다.  
아니면 그 프라이빗 마저 더 쪼개서 퍼블릭으로 만들란 소린가...;; 모르겠당.  

간단한 reflection을 이용하여 private 메서드를 테스트하는 예제로 마무리 해야겠다.

```java
public class Service {
    private static boolean serve() {
        return true;
    }

    private static boolean serve2(boolean bool) {
        return bool;
    }
}
```

```java
public class ServiceTest {
    private Service service;

    @Before
    public void setup() throws IllegalAccessException, InstantiationException {
        service = Service.class.newInstance();
    }

    @Test
    public void test() throws InvocationTargetException, IllegalAccessException, NoSuchMethodException {
        Method method = service.getClass().getDeclaredMethod("serve");
        method.setAccessible(true);

        assertTrue((boolean) method.invoke(service));

        method = service.getClass().getDeclaredMethod("serve2", boolean.class);
        method.setAccessible(true);

        assertTrue((boolean) method.invoke(service, true));
        assertFalse((boolean) method.invoke(service, false));
    }
}
```
