---
title: Redis 간단 정리 01
date: 2018-06-26 02:45:25
tags: [NoSQL, Cache, Redis]
---

## 저장된 모든 키 보기
```bash
redis-cli
keys *
```

위와 같이 하면 아래와 같이 나옴.
```
1) "\xac\xed\x00\x05t\x00\aLeisure"
```
RedisTemplate을 이용해서 넣은 GeoSpacial  
나는 분명 키를 Leisure로 넣었는데 앞에 요상한 게 붙는다.  
redis-cli를 통해 넣으면 저렇게 안 나옴.

## GeoSpacial의 타입
```bash
redis-cli
type Leisure
```
zset이라고 나온다.  

[geopos command](https://redis.io/commands/geopos)에도 아래와 같이 나온다.  
> geospatial index represented by the sorted set at key  

위 내용을 봐서 sorted set임이 틀림 없다.  

## GeoSpacial 용량 확인하기
딜이 만개라고 가정했을 때 만개의 좌표를 넣어보고 메모리를 봐보자.  
```bash
for i in {0..9999}; do redis-cli GEOADD Leisure 13.361389 38.115556 $i; done
redis-cli
memory usage Leisure
```
[memory usage](https://redis.io/commands/memory-usage)는 해당 키/밸류가 차지하고 있는 메모리의 byte를 반환한다. 
958675 byte = 0.9mb, 이거 뭐 아주 그냥 코딱지 만큼 들어간다.

## expire set
```bash
redis-cli
expire Leisure 10
```
[expire](https://redis.io/commands/expire) documentation을 보면 된다.  
키, 초를 입력하면 된다.  
[ttl(남은 초 확인)](https://redis.io/commands/ttl)과 [pttl(남은 ms 확인)](https://redis.io/commands/pttl)로 확인 가능하다.

흠냐... 빨리 자자...