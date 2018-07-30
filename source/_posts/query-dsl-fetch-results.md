---
title: (QueryDSL) fetchResults
date: 2018-07-09 23:43:43
tags: [JPA, QueryDSL]
---

[QueryDSL](http://www.querydsl.com/)은 Dynamic Query를 만들어주는 Query Builder이다.  
기존에 [Jooq](https://www.jooq.org/)를 사용해보긴 했지만 Jooq는 ORM이 아니라 JPA와 뭔가 잘 맞지 않을 것 같았다.  
그러다보니 페이지네이션도 뭔가 짜칠 거 같고 JPA에서 제공해주는 객체 그래프 탐색 등등의 용이함을 이용할 수 없을 것 같아서 QueryDSL을 선택했다.  
하지만 [Is querydsl dead?](https://github.com/querydsl/querydsl/issues/2170)란 이슈가 올라올 정도로 제대로 프로젝트가 관리되고 있지 않다.  

## 문제
일단 QueryDSL을 사용하고 있는 프로젝트가 규모가 크지 않고, ~~지금 짜는 코드만 잘 돌아가면 됐지~~란 생각으로 코딩 중이었다.  
하지만 당장 맞닥뜨린 문제는 [JPA fetchCount() and group by not working](https://github.com/querydsl/querydsl/issues/1614)이었다.  
간단한 예시를 보자.  

```java
@Repository
@RequiredArgsConstructor
public class LeisureQueryDslRepository {
    @PersistenceContext
    private final EntityManager entityManager;

    public Page<Leisure> findAllBy(final List<Long> dealIds, final LeisureCriteria criteria, final Pageable page) {
        QLeisure leisure = QLeisure.leisure;
        final JPAQuery<Leisure> query = new JPAQueryFactory(entityManager).selectFrom(leisure);

        // 에러 발생 안함
        final long count = query.fetchCount();
        
        query.groupBy(leisure.id)
             .having(leisure.id.count().eq(1L));
        
        // 에러 발생함
        final long countWithGroupBy = query.fetchCount();

        return new PageImpl<>(query.fetch(), page, query.fetchCount());
    }
}
```

아래와 같은 에러 메시지가 나온다.  
>> org.hibernate.hql.internal.ast.QuerySyntaxException: unexpected token: having near line 3, column 1 [select count(distinct leisure.id)
   from com.leisureq.map.v5.domain.deal.leisure.Leisure leisure
   having count(leisure.id) = ?1]

나는 분명 groupBy도 넣었는데 저런 오류가 나온다.  
위 이슈를 fix한 [풀리퀘](https://github.com/querydsl/querydsl/pull/1619)도 있고, 메인테이너가 날린 건데 아직도 머지가 되지 않았다 -_-;;  

fetchCount 대신에 아래와 같이 fetchResults()를 사용하면 오류를 피할 수 있다.  
```java

```

