---
title: "Javascript로 동적 select option 만들기"
date: 2021-09-10
categories: Javascript
---

### js로 동적 select option 만들기

---

form에서 select option을 자바스크립트로 만드는 방법을 알아보자.

이번 포스팅에서 만드려고 하는 select option은 첫번째 옵션을 셀렉트 하면
두번째 옵션이 첫번째 옵션에 맞는 내용으로 작성되게 해볼 것이다.

```
<form action="" method="post">
    상품코드 <select name="code" id="select_code" onChange="change_code()"></select>
    <!-- 상품코드 : A,B,C,D -->
    상품카테고리 <select name="category" id="select_category"></select>
    <!-- 상품카테고리 : A(A1,A2,A3),B(B1,B2,B3),C(C1,C2,C3),D(D1,D2,D3) -->
</form>
```

상품코드를 A를 선택 했을 때 상품카테고리는 A1, A2, A3을 선택할 수 있게 하고
상품코드를 D를 선택 했을 때 상품카테고리는 D1, D2, D3을 선택할 수 있게 해보겠다.

자바스크립트 코드로 아래와 같이 작성한다.

```
window.onload = function(){
	const code = ['A','B','C','D'];
	
	document.getElementById('select_code').options[0] = new Option('상품코드를 선택하세요','');
	document.getElementById('select_category').options[0] = new Option('상품카테고리를 선택하세요','');
	
	for(i=0;i<code.length;i++){
		document.getElementById('select_code').options[(i+1)] = new Option(code[i]);
	}
}

function change_code(){
	const category = [['A1','A2','A3'],['B1','B2','B3'],['C1','C2','C3'],['D1','D2','D3']];
	const code_index = document.getElementById('select_code').selectedIndex;
	
    <!-- 상품코드에 변화가 생길 경우 상품카테고리를 초기화 -->
	for(i=document.getElementById('select_category').length;i>0;i--){
		document.getElementById('select_category').options[i]=null;
	}
	
	for(i=0;i<category[(code_index-1)].length;i++){
		document.getElementById('select_category').options[(i+1)] = new Option(category[code_index-1][i]);
	}
}
```


