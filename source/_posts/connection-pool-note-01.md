---
title: Apache Commons Generic Object Pool 간단 정리
date: 2018-06-26 10:26:59
tags: [Connection Pool]
---
Connection Pool이라 하면 미리 커넥션을 맺어놓고 필요할 때 마다 일일이 커넥션을 새로 맺지 않고 해당 커넥션을 가져다 쓰는 기술.  
기본적으로 Connection을 맺는 것 자체도 상당한 비용을 소모하므로 위와 같은 기술이 등장한 듯?

Jedis의 connection pool은 apache commons의 GenericObjectPool을 쓰는 듯  
GenericObjectPool에는 maxIdle, minIdle, maxTotal이 있다.  
Idle은 커넥션 풀에서 대기 상태로 있는 애를 뜻하는 것 같다.  
maxTotal이 10이고, maxIdle이 5면 6개를 borrow 할 때 새로 커넥션을 맺는 듯...  
그리고 return 할 때 다시 커넥션을 끊고...  
따라서 maxTotal과 maxIdle은 동일한 게 이상적일 듯...  
그럼 minIdle은 initialSize를 뜻하는 걸까??  
초기에는 minIdle 만큼 커넥션을 맺어놓고 추후에 maxIdle까지 커넥션이 생성되는 걸까?  
아니면 maxIdle까지 갔다가 일정시간이 지나면 다시 minIdle까지 줄어드는 걸까...?
잘 모르것당 ㅎㅎ

borrow는 커넥션 풀에서(혹은 새로운 커넥션을 맺든) 커넥션을 빌려온다는 뜻인 것 같다.  
return은 커넥션 풀에 반납한다는 뜻 같고,  
release는 return 시에 커넥션 풀이 꽉 찼을 때 해당 커넥션을 해방(?)시켜줄 때 쓰는 표현 같다.