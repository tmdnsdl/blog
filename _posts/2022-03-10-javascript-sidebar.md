---
title: "Javascript 사이드바 제작에 대해 알아보자"
date: 2022-03-10
categories: Javascript
---

### Javascript Sidebar

---

웹 페이지 제작에 많이 쓰이는 3단 메뉴로 구성된 사이드바를 제작해보자.
jQuery를 이용하여 사이드바를 제작하는 법을 알아보겠다.

---

**jQuery**

```
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
$(document).ready(function() {
   $(".menu>a").click(function() {
      let submenu = $(this).next("ul");
      let othermenu = $(".sidebar .nav>li>a").next("ul").not(submenu);
      if(submenu.is(":visible")) {
         submenu.slideUp();
      } else {
         submenu.slideDown();
         othermenu.slideUp();
      }
   });

   $(".sub-menu>a").click(function() {
      let submenu = $(this).next("ul");
      let othermenu = $(".sub-menu li>a").next("ul").not(submenu);
      if(submenu.is(":visible")) {
         submenu.slideUp();
      } else {
         submenu.slideDown();
         othermenu.slideUp();
      }
   });
});
```

위의 코드의 jQuery slideUp, slideDown 기능을 이용하여
메뉴를 접고 펼치는 3단 메뉴를 제작 할 수 있다.

---

**html**

```
<div class="sidebar-container">
    <div class="sidebar">
        <div>
            <ul class="nav">
            <li>
                <span>페이지명</span>
            </li>
            <li class="menu">
                <a href="javascript:;">
                <b class="caret"></b>
                <span>대메뉴</span>
                </a>
                <ul style="display: none">
                <li class="sub-menu">
                    <a href="javascript:;">
                    <b class="caret"></b>
                    <span>중메뉴</span>
                    </a>
                    <ul style="display: none">
                    <li>
                        <a href="javascript:;">
                        <span>소메뉴</span>
                        </a>
                    </li>
                    </ul>
                </li>
                </ul>
            </li>
            </ul>
        </div>
    </div>
</div>
```

위의 html 코드와 jQuery의 기능으로 3단으로 구성된 메뉴를 제작 할 수가 있다.
css를 추가하여 나만의 3단 메뉴를 만들어보자.
