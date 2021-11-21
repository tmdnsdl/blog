---
title: "Javascript 변수 선언에 대해"
date: 2021-11-22
categories: Javascript
---

### javascript 변수 선언 : var

---

javascript에서 ES6 이전에 사용되었던 변수 선언은 var를 이용하는 것 이었는데 문제가 많아 ES6에서 let, const로 변수 선언이 가능해졌다.

var는 꽤나 헷갈리는 변수 선언 방식이라고 할 수 있는데 먼저 var로 변수 선언할 경우에 var 키워드를 생략하고 변수를 선언할 수가 있다.

```
raccoon = '너구리';
// var raccoon = '너구리';
// 두가지 방식으로 변수 선언 가능
```

또한 var는 변수를 선언 후에 변수 중복 선언이 가능하다.

```
var raccoon = '너구리';
raccoon = '라쿤';
// raccoon의 값은 라쿤으로 바뀐다
```

var의 변수 선언은 함수의 코드 블록만을 스코프(Function-level scope)로 인정하고 함수 내부에서 생성한 변수는 지역 변수 이지만 함수 외에서 선언한 변수는 모두 전역 변수가 된다.

---

### javascript 변수 선언 : let / const

---

var로 변수 선언하는 것이 문제가 많아서 javascript ES6에서는 새롭게 let / const 키워드를 제공하여 변수 선언을 할 수 있게 되었다.

let / const의 특징은 블록 레벨 스코프(Block-level scope)로 var의 경우는 함수 외에서 선언한 변수가 모두 전역 변수가 되는 함수 레벨 스코프를 가지지만 let / const는 코드 블록(함수, if, for 등) 내에서 선언된 변수는 코드 블록 내에서만 유효한 지역 변수로 설정이 된다.

```
let raccoon = '라쿤';
{
    let raccoon = '너구리';
    console.log(raccoon); // 너구리
}
console.log(raccoon); // 라쿤
```

또한 var와 let / const의 차이점은 변수 중복 선언이 불가능하다는 점이다.

---

let / const의 차이점은 let은 변수 선언 후 값을 재할당 가능하고 const는 상수이므로 값을 재할당 할 수 없다는 차이점이 있다.

```
let raccoon = '라쿤';
raccoon = '너구리';
// raccoon = 너구리

const raccoon2 = '라쿤';
raccoon2 = '너구리';
// const는 상수이므로 재할당 불가
```

변수를 선언하는 경우 ES6이라면 let / const를 사용하고 var는 사용하지 않는 것이 바람직하다. 
기본은 상수인 const를 사용하여 의도하지 않은 변수의 재할당을 방지하도록 하고 변수의 재할당이 필요한 경우에만 let을 사용하면 되겠다.

---
