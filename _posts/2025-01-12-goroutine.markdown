---
layout: post
title: "goroutine"
date: 2025-01-12 10:26:52 +0900
categories: golang packages
---

# goroutine

1 cpu (core) 가 여러 개의 스레드를 컨텍스트 스위칭으로 실행 ⇒ 컨텍스트 스위칭 비용 발생.

goroutine: 1 core에 1개의 스레드만 할당 되도록 함 ⇒ 컨텍스트 스위칭 비용 발생하지 않음

단, 1cpu ~ 1 core ~ 1 thread ~ 1 goroutine 으로 고정되어 있기 때문에,

goroutine 개수 > core 수 라면,

해당 스레드에 걸려있는 고루틴 작업이 완료가 되어야 새로운 고루틴이 스레드에 들어갈 수 있음

단, thread에 붙어있는 고루틴이 시스템 콜 호출로 인해 대기 상태가 되면,

잠시 빠져나와 대기중인 고루틴에게 자리를 빌려줄 수 있다. (cpu 자원 낭비를 막아야 하기 때문이다.)

## waitGroup

### wg.Add(작업 수)

```go
wd.Add(3) //작업 할 고루틴의 수가 3개
```

### wg.Done()

```go
해당 goroutine에 걸려있는 작업이 끝났음을 알림 => wg.Add(n) 에 등록한 작업을 1개씩 차감함
```

### wg.Wait()

```go
wg.Add로 등록한 모든 고루틴 작업이 끝날때까지, 이 밑의 줄은 실행하지 않고 기다림
```
