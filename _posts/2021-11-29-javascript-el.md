---
title: "Javascript 템플릿 리터럴이란?"
date: 2021-11-29
categories: Javascript
---

### javascript template literals

---

전에 알아본 JSP의 EL (Expression Language) 코드와 같이 javascript에서도 사용할 수 있는 표기법인 템플릿 리터럴을 알아보도록 하겠다.

템플릿 리터럴은 ES6부터 새로 도입된 문자열 표기법이며 JS에서 문자열에 사용되는 ""이 아닌 (`)을 사용하여 표기하게 된다.
또한 표현식을 삽입할 수 있는 기능을 제공한다.

---

- **일반 문자열 표기법**

```
const a = "너구리";
const b = "라쿤";
const str = b+"은 "+a+"가 아닙니다.";
const str2 = b+"은\n"+a+"가 아닙니다.";

console.log(str);
// 라쿤은 너구리가 아닙니다.
console.log(str2);
// 라쿤은 
너구리가 아닙니다.

// 일반 문자열 표기법은 띄어쓰기 작성이 불편하며 
가독성이 떨어진다.
또한 줄바꿈을 하고 싶은 경우 \n 작성이 필요하다.
```

---

- **템플릿 리터럴**

```
const a = "너구리";
const b = "라쿤";
const str = `${b}은 ${a}가 아닙니다.`;
const str2 = `${b}은 
${a}가 아닙니다.`;

console.log(str);
// 라쿤은 너구리가 아닙니다.

console.log(str2);
// 라쿤은 
너구리가 아닙니다.

// 템플릿 리터럴은 줄바꿈을 하기가 쉬우며
표현식을 사용할 수 있어 가독성이 좋다.
```

---
