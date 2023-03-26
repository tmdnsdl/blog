---
title: "Spring 서비스 시작 시 이벤트 처리"
date: 2023-03-21
categories: Spring
---

### Spring 서비스 시작 시 프로그램 동작 이벤트 처리

---

스프링 서비스 시작을 감지하여 동작하는 메소드 예제를 알아보자.

```
@EventListener(ContextRefreshedEvent.class)
public void contextRefreshedEvent(ContextRefreshedEvent event) {
    if (!event.getApplicationContext().equals(this.applicationContext)) {
        return;
    }

    // 서비스 추가
}
```
ContextRefreshedEvent는 ApplicationContext(스프링 컨테이너)를 초기화하거나 새로 고칠 경우에 이벤트를 감지하여 해당 메소드가 동작하게 된다.

위의 메소드를 사용하여 처음 시작할 기능에 대해 정의할 수 있다.
