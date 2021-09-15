---
title: "JAVA List/Map 개념 정리"
date: 2021-09-08
categories: Java
---
### 컬렉션 / 맵

---

자바 컬렉션 프레임워크에서 제공하는 인터페이스

자바에서 배열이 고정된 크기의 메모리를 가지는 것과 달리
컬렉션 / 맵은 동적으로 메모리를 확장하며 객체를 저장한다

자바 컬렉션 프레임워크의 핵심 인터페이스로는 
`List / Set / Map`이 존재한다.

---

* __List__

List 인터페이스는 순서대로 데이터가 저장되며 데이터를 중복해서 포함할 수 있는 특징을 가진다.
List 인터페이스를 구현하는 클래스는 ArrayList, LinkedList, Stack, Vector 등이 있다.

ArrayList는 Vector를 개선한 클래스이다.
차이점은 Vector는 자체적으로 동기화를 하는 반면 ArrayList는 동기화 처리를 하지 않는다

ArrayList는 순차적으로 데이터를 추가하거나 삽입하는 경우에는 빠르지만
배열의 중간에 Element의 삽입/삭제를 할 경우에는 LinkedList를 이용하는 것이 효과적이다.

* __Set__

Set 인터페이스는 순서 없이 데이터가 저장되며 데이터를 중복해서 포함할 수 없다.
Set 인터페이스를 구현하는 클래스에는 HashSet, TreeSet 등이 있다.

HashSet은 해시테이블에 Element를 저장하므로 성능면에서 가장 우수하다.
저장 순서를 유지하고 싶은 경우 해시테이블과 연결리스트를 결합한 LinkedHashSet을 사용한다.
TreeSet은 검색을 해야할 경우 사용하며 Set과 Map 인터페이스를 상속받아 정렬기능을 가진다.

* __Map__

Map 인터페이스는 검색의 개념이 추가된 인터페이스로 List,Set이 value만 저장하는 구조인 것과 달리
Map은 key / value를 저장하는 구조를 가지며 key를 이용하여 value를 검색 할 수 있게 된다.
Map 인터페이스는 데이터 삽입 시 순서는 유지하지 않고 key는 중복이 안되며 value는 중복을 허용하는 구조를 가진다.

HashMap 클래스는 Map 인터페이스의 대표적인 클래스로 동기화가 필요없을 경우에 사용한다.
TreeMap 클래스는 TreeSet과 같이 Set과 Map 인터페이스를 상속받아 정렬기능을 가진다.
