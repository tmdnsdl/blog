---
title: "Javascript 비교 연산자"
date: 2021-11-30
categories: Javascript
---

### javascript 비교 연산자의 차이

---

javascript에서 비교 연산자는 == / === 두가지 방식을 사용할 수 있다.

== 는 비교하는 값이 같은지를 비교하여 값이 같으면 true, 다르면 false로 처리한다.

반면 === 의 경우에는 비교하는 값과 값의 데이터 타입이 같은지 까지 비교하는 연산자로 사용된다.

```
const a = 1;
const b = "1";

console.log(a==b); // 값이 같으므로 true를 리턴
console.log(a===b); // 값이 같지만 데이터 타입이 달라 false를 리턴

console.log(null==undefined); // 둘다 값이 없음 true를 리턴
console.log(null===undefined); 
// 둘다 값이 없지만 데이터 타입은 다르므로 false를 리턴

console.log(true == 1); // true는 1이므로 true를 리턴
console.log(true === 1); 
// 둘다 값은 1이지만 데이터 타입이 달라 false를 리턴

```

---
