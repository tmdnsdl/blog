---
title: "Javascript로 모달 윈도우 만들기"
date: 2022-07-15
categories: Javascript
---

### Create Modal Window

---

웹 페이지에서 사용자의 관심을 끌어야하는 기능이나 복구가 불가능한 수정, 선택을
하려는 경우 사용하면 좋은 모달 윈도우에 대해서 예제를 통해 알아보자

---

**Javascript**

```
<script type="text/javascript">
    function search() {
        const bg = document.createElement("div");
        bg.setAttribute("class", "modal-bg");
        bg.setAttribute("onclick", "closeFunction()");

        const search_box = document.createElement("div");
        search_box.setAttribute("class", "search-box");

        const title = document.createElement("div");
        title.style.display = "flex";
        title.innerHTML = `
        <h3>title</h3>
        <h3 class="icon-close" onclick="closeFunction()">X</h3>
        `;

        search_box.append(title);

        const content = document.createElement("div");
        content.innerHTML = `
        <div>
            <p>put contents in here</p>
        </div>
        `;

        search_box.append(content);

        document.body.append(bg);
        document.body.append(search_box);
        document.body.classList.add("stop-scroll");
    }

    function closeFunction() {
        const bg = document.getElementsByClassName("modal-bg");
        const search_box = document.getElementsByClassName("search-box");

        bg[0].remove();
        search_box[0].remove();
        document.body.classList.remove("stop-scroll");
    }
</script>
```

---

**html & css**

```
<style>
    .search-box {
        position: fixed;
        width: 500px;
        height: 200px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        padding: 3rem;
        background: white;
        border-radius: 0.8rem;
        z-index: 9;
    }
    .modal-bg {
        position: fixed;
        z-index: 8;
        display: block;
        width: 100vw;
        height: 100vh;
        left: 0;
        top: 0;
        opacity: 0.3;
        background: #000;
    }
    .stop-scroll {
        height: 100%;
        min-height: 100%;
        overflow: hidden !important;
        touch-action: none;
    }
    .icon-close {
        margin-left: auto;
        padding: 3px;
        cursor: pointer;
        border: 1px solid gray;
    }
</style>

<div class="modal-box">
    <button type="button" onclick="search();">검색</button>
</div>
```

해당 예제는 검색 버튼을 클릭하면 주변 배경이 블러 처리 되면서 모달 윈도우가 생성되는 예제이다.
스크롤바를 비활성화 시키고 모달 윈도우를 화면 가운데에 위치하게 하여 사용자에게 내용을 확인 시킬 수 있다.

사용자는 닫기 버튼이나 블러 처리된 배경을 클릭하여 모달 윈도우를 닫아야만 기존 웹 페이지로 돌아갈 수 있고
모달 윈도우를 닫기 전까지는 모달 윈도우의 내용에 집중하게 된다.

원하는 기능을 추가하여 사용자의 관심이 필요한 항목이나 웹 관리자의 수정, 삭제 등의 기능에 유용하게 활용이 가능하다.
