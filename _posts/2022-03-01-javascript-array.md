---
title: "Javascript 배열 문법을 알아보자"
date: 2022-03-01
categories: Javascript
---

### Javascript 기초 배열 문법

---

Javascript에서 많이 쓰이게 되는 배열의 문법에 대해서 알아보자
배열 안의 데이터를 핸들링 할 때 간략하고 편하게 사용할 수 있는 방법을 알아보겠다.

```
<script>
    // 일반적인 배열 데이터
    const raccoon = ["너구리", "라쿤"];
    const nu = raccoon[0];
    const ra = raccoon[1];

    console.log(nu); // 너구리
    console.log(ra); // 라쿤

    // 간략한 배열 문법 사용
    const raccoon = ["너구리", "라쿤"];
    const [nu, ra] = raccoon;

    console.log(nu); // 너구리
    console.log(ra); // 라쿤
</script>
```

자바스크립트에서 배열은 많이 사용하게 되는데 위와 같은 방법으로
보다 편리하게 배열의 데이터를 핸들링 할 수 있는 장점이 있다.
