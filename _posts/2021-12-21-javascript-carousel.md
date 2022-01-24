---
title: "Javascript 캐러셀 슬라이드 구현"
date: 2021-12-21
categories: Javascript
---

### Javascript 캐러셀 슬라이드

---

자바스크립트 라이브러리인 jQuery 기반 캐러셀 슬라이드인
Owl Carousel을 사용하여 슬라이드 효과를 구현해보자.

---

**Setup**

```
<head>
    <link rel="stylesheet" href="owlcarousel/owl.carousel.min.css">
    <link rel="stylesheet" href="owlcarousel/owl.theme.default.min.css">
</head>
<footer>
    <script src="jquery.min.js"></script>
    <script src="owlcarousel/owl.carousel.min.js"></script>
</footer>
```

https://owlcarousel2.github.io/OwlCarousel2/ 에서 파일 다운로드가 가능하다.

html head 태그 안에 css 파일을 링크해준다.
footer 태그 안에 js 파일을 링크해 준다.

owlCarousel을 jquery 밑에 작성하여야 제대로 불러온다.
jQuery는 1.8.3 버전 이상을 사용해야 한다.

---

**Javascript**

```
$(function(){
    $('.owl-carousel').owlCarousel({
    items:1,
    nav:true,
    loop:true,
    mouseDrag:false,
    //animateOut: 'fadeOut'
    });
});
```

스크립트에 owlCarousel 설정을 작성한다.
owlCarousel API 옵션은 아래의 링크에서 확인 할 수 있다.
<https://owlcarousel2.github.io/OwlCarousel2/docs/api-options.html>

---

**Html**

```
<div class="owl-carousel">
    <div class="item">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
    </div>
    <div class="item">
        <div>6</div>
        <div>7</div>
        <div>8</div>
        <div>9</div>
        <div>10</div>
    </div>
</div>
```

item에 값을 주어 슬라이드를 설정할 수 있다.
현재 설정은 item 1개 씩 슬라이드 되도록 설정이 되어
한 페이지에 5개의 값을 보여주는 영역을 하나의 슬라이드로 보여지게 되있다.

item 설정은 다양하게 할 수 있으며 5개를 설정하여 하나의 슬라이드로 보이게 할 수 있다.

---

**CSS**

```
<div class="owl-carousel owl-loaded">
    <div class="owl-stage-outer">
        <div class="owl-stage">
            <div class="owl-item">...</div>
            <div class="owl-item">...</div>
            <div class="owl-item">...</div>
        </div>
    </div>
    <div class="owl-nav">
        <div class="owl-prev">prev</div>
        <div class="owl-next">next</div>
    </div>
    <div class="owl-dots">
        <div class="owl-dot active"><span></span></div>
        <div class="owl-dot"><span></span></div>
        <div class="owl-dot"><span></span></div>
    </div>
</div>
```

owlCarousel을 페이지에 맞게 구현하기 위해 CSS를 활용해야 한다.
사이즈 및 위치를 조정하여 페이지에 맞게 지정한다.
