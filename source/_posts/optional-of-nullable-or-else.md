---
title: (Java) Optional로 NULL 처리
date: 2018-07-03 01:42:30
tags: [Java, Optional]
---
Java8에서 등장한 Optional 클래스, NULL로 인해 생기는 문제들을 얘로 해결해보자.  

```java
public class Ttest {
    @Test
    public Long test(Deal deal) {
        return deal.getCategoryMapList().get(0).getCategoryTree().getCategoryGroup().getId();
    }
}
```

어디서 NPE가 터질지 모른다.  
아래와 같이 일일이 체크해야한다.  

```java
public class Ttest {
    @Test
    public Long test(Deal deal) {
        if(deal == null) return null;
        if(CollectionUtils.isEmpty(deal.getCategoryMapList())) return null;
        if(deal.getCategoryMapList().get(0) == null) return null;
        if(deal.getCategoryMapList().get(0).getCategoryTree() == null) return null;
        if(deal.getCategoryMapList().get(0).getCategoryTree().getCategoryGroup() == null) return null;
        if(deal.getCategoryMapList().get(0).getCategoryTree().getCategoryGroup().getId() == null) return null;
        return deal.getCategoryMapList().get(0).getCategoryTree().getCategoryGroup().getId();
    }
}
```

코드가 매우 구려졌다.  
이를 그럼 자바 8스럽게, 우아하게 Optional로 처리해보자.  

```java
public class Ttest {
    @Test
    public Long test(Deal deal) {
        return Optional.ofNullable(deal)
                       .map(deal -> CollectionUtils.isEmpty(deal.getCategoryMapList()) ? null : deal.getCategoryMapList())
                       .map(categoryMapList -> categoryMapList.get(0))
                       .map(categoryMap -> categoryMap.getCategoryTree())
                       .map(categoryTree -> categoryTree.getCategoryGroup())
                       .map(categoryGroup -> categoryGroup.getId())
                       .orElse(null);
    }
}
```

if를 태우는 거보다 훨씬 가독성이 좋다고 생각한다.  
Optional 체이닝 중에 중간에 null을 리턴하게 하면 orElse로 점프를 뛰게 된다.

아래와 같이 null이면 exception을 throw 할 수도 있다.
```java
public class Ttest {
    @Test
    public void test(Deal deal) {
        Optional.ofNullable(deal)
                .map(deal1 -> CollectionUtils.isEmpty(deal1.getCategoryMapList()) ? null : deal1.getCategoryMapList())
                .map(categoryMapList -> categoryMapList.get(0))
                .map(categoryMap -> categoryMap.getCategoryTree())
                .map(categoryTree -> categoryTree.getCategoryGroup())
                .map(categoryGroup -> categoryGroup.getId())
                .orElseThrow(() -> new IllegalArgumentException(deal.dealCategory.getCategory1()));
    }
}
```

null을 핸들링 할 때 앞으로 자주 애용해야겠다.  
JPA도 Optional로 리턴할 수 있으니 앞으로 Optional로 무조건 받아서 처리하자.  
```java
@Repository
public interface HotelRepository extends PagingAndSortingRepository<Hotel, Long> {
    Optional<Hotel> findById(long id);
}
```
