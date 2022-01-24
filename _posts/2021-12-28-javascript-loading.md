---
title: "Javascript으로 페이지 로딩 구현"
date: 2021-12-28
categories: Javascript
---

### javascript 페이지 로딩

---

파일을 첨부하여 업로드 할 시에 파일 용량이 크다면 현재 페이지에서 로딩 처리를 해야 할 경우가 있다.
현재 프로세스가 진행 중이라는 것을 웹 페이지에서 알려주기 위해 로딩 페이지를 구현 해보았다.

페이지 전체 화면 기준으로 처리되며 정중앙에 로딩 이미지가 나오게 된다.
화면 사이즈와 상관 없이 로딩 이미지가 반응형으로 정중앙에 위치하게 된다.

화면의 넓이와 높이는 다른 사이즈로 설정할 수 있으며 이미지 크기도 설정할 수 있다.
현재 코드에서는 아이폰 로딩 이미지를 사용하여 구현하였다.

로딩 이미지 다운 경로 : gifer.com/en/gifs/loader

---

```
function loading() {
    const mask = document.createElement("div");
    mask.style.cssText =
        "position:absolute; z-index:9; display:block; left:0; top:0;";

    // 화면 넓이, 높이 설정
    mask.style.width = "100vw";
    mask.style.height = "100vh";

    // 화면 투명도 설정
    mask.style.opacity = "0.3";

    // 화면 배경색 설정
    mask.style.backgroundColor = "#000000";

    const img = document.createElement("img");
    img.setAttribute("src", "images/loading.gif"); // 로딩 이미지 경로 설정
    img.style.cssText = "position: relative; display: block; margin: 0px auto;";

    // 이미지 크기 설정
    img.style.width = "50px";
    img.style.height = "50px";

    const loadingImg = document.createElement("div");
    loadingImg.setAttribute("id", "loadingImg");
    loadingImg.style.cssText =
        "position:absolute; z-index:9; display:block; left:50%; top:50%;";

    // 이미지 화면 중앙정렬 설정
    loadingImg.style.width = img.style.width;
    loadingImg.style.height = img.style.height;
    loadingImg.style.marginLeft =
        (loadingImg.style.width.replace("px", "") / 2) * -1 + "px";
    loadingImg.style.marginTop =
        (loadingImg.style.height.replace("px", "") / 2) * -1 + "px";

    loadingImg.append(img);

    // 페이지에 로딩 화면 설정
    document.body.append(mask);
    document.body.append(loadingImg);
}

```

---
