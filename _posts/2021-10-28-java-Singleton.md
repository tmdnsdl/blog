---
title: "Java 싱글톤 패턴이란?"
date: 2021-10-28
categories: Java
---

### Java 싱글톤(Singleton) 패턴

---

싱글톤 패턴은 인스턴스가 오직 1개만 생성되야 하는 경우에 사용되는 디자인 패턴이다.
객체가 여러개 생성되면 값이 바뀌어 에러가 나거나 하는 상황에 쓰인다.

인스턴스가 한개만 생성되므로 하나의 인스턴스를 메모리에 등록하여 여러 스레드(멀티스레드)에서 동시에
해당 인스턴스를 공유하여 사용할 수 있으므로 효율을 높일 수 있다는 장점이 있다.
하지만 여러 스레드에서 쓰이게 되는 경우 충돌의 우려가 있으므로 동시성 문제를 고려하여야 한다.

자바에서는 클래스의 생성자를 private로 지정하여 사용하고 static method로 인스턴스를 생성하게 된다.

```
public class Person {
	private Person() {
		// 생성자
	}
	private static Person person;
	public static Person getInstance() {
		if(person==null) {
			person = new Person();
		}
		return person;
	}
}
```

위와 같이 싱글톤 패턴을 구현할 수 있는데 위의 예제는 동시성 문제를 고려하지 않은 싱글톤 패턴이다.
싱글톤 패턴을 구현할 경우에는 동시성 문제를 고려하여 Thread-safe하게 구현되어야 한다.

Thread-safe하게 싱글톤 패턴을 구현하는 방법 중 LazyHolder(static holder) 방식이 있다.

```
public class Person {
	private Person() {
		// 생성자
	}
	private static class SingletonInstance() {
		// 클래스 로딩 시 생성
		private static final Person person = new Person();
	}
	
	public static Person getInstance() {
		return SingletonInstance.instance;
	}
}
```

위와 같은 LazyHolder 방식은 동시성 문제를 고려한 싱글톤 패턴이며 
Synchronized를 적용한 방식 등에 비해 성능 면에서 이점이 있으며
Java로 싱글톤 패턴을 구현할 경우 가장 많이 쓰이는 방식이기도 하다.