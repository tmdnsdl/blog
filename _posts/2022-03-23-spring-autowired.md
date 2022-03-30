---
title: "스프링 생성자 주입에 대해 알아보자"
date: 2022-03-23
categories: Spring
---

### Spring Constructor Injection

---

스프링 프로젝트에서 의존성을 주입하는 방법으로 Autowired 어노테이션이 많이 이용된다.
하지만 스프링에서는 autowired가 아닌 생성자를 통한 주입을 권장하고 있기에
이번에는 스프링 생성자 주입에 대해서 알아보도록 하자.

---

**Spring 생성자 주입**

> Spring Team recommends: "Always use constructor based dependency injection in your beans.
> Always use assertions for mandatory dependencies"

스프링에서는 Autowired 어노테이션을 이용한 필드 주입 보다
생성자를 통한 주입을 사용하는 것을 권고하고 있다.

생성자를 통한 주입 방식의 장점으로는

1. 순환 참조를 방지
2. final을 선언하여 불변성을 보장
3. 테스트 코드를 작성하기가 좋음

이라는 장점이 있기 때문에 스프링에서도 생성자 주입을 권고하고 있다.

---

**@Autowired 방식**

```
@RestController
public class TestController {

    @Autowired
    private Mapper mapper;
}
```

Autowired 어노테이션의 경우 많이 이용되었지만 외부에서 객체를 변경할 수 없는
단점으로 인해 테스트 코드가 중요해진 현재는 추천되지 않는 방식이다.

---

**생성자 주입 방식**

```
@RestController
public class TestController {

    private final Mapper mapper;

    // 생성자가 하나 일 경우 @Autowired 생략 가능
    public TestController(Mapper mapper) {
        this.mapper = mapper;
    }
}
```

생성자 주입 방식은 스프링에서도 권고하는 의존성 주입 방식이고
개발 시에 여러 장점이 있기 때문에 생성자 주입 방식을 이용해야 되겠다.
