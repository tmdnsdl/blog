---
title: "Javascript 첨부파일 추가 기능 구현"
date: 2022-01-17
categories: Javascript
---

### Javascript 첨부파일 추가

---

첨부파일 추가를 새로고침 없이 삭제도 가능하게 구현하는 방법에 대해 알아보자.

---

**Html**

```
<div>
    <div id="file_add">
        <button type="button" class="bt-common" onclick="addFiles()">파일 추가</button>
    </div>
    <div id="file_preview"></div>
</div>
```

버튼 디자인은 bt-common 클래스로 CSS 설정을 바꿔줄 수 있다.

---

**Javascript**

```
let addIndex = 1;

// 첨부파일 추가
function addFiles() {
    const fileId = "attachFile" + addIndex;
    $("#file_add").append("<input type='file' name='file' id='"+fileId+"' onchange='previewFile(this)' style='display:none;'>");
    // 첨부파일 추가 버튼을 클릭할 경우 새로운 input file을 생성

    const clickFile = document.getElementById(fileId);
    clickFile.click();

    addIndex++;
}

// 등록 파일 미리보기
function previewFile(ele) {
    const preview = document.getElementById("preview");
    const fileId = ele.id; // input file 아이디 값
    const file = document.getElementById(fileId).files; // 등록한 파일
    const fileName = file[0].name; // 등록한 파일명
    const deleteClass = 'D' + fileId; // 파일 삭제 버튼 기능 구현을 위한 클래스명 지정

    let str ="<div class='"+deleteClass+"'>";
    str += "파일명: " + fileName;
    str += "<button type='button' class='bt-delete ico'></button></div>";
    preview.innerHTML += str;

    const fileDiv = document.getElementsByClassName(deleteClass);
    const fileButton = fileDiv[0].querySelector('button');
    fileButton.setAttribute("onclick", "deleteFiles('"+deleteClass+"')");
}

// 등록 파일 삭제
function deleteFiles(ele) {
    if(confirm("파일을 삭제 하겠습니까?") == true) {
        const fileName = document.getElementsByClassName(ele);
        fileName[0].remove();

        const fileId = ele.replace("D", "");
        const fileReset = document.getElementById(fileId);
        fileReset.value = "";
    }
}
```

첨부파일 삭제 버튼의 bt-delete ico 클래스를 이용하여 버튼을 꾸밀 수 있다.

<https://fonts.google.com/icons?selected=Material+Icons>에서 다양한 아이콘을 다운받을 수 있다.

첨부파일 추가 버튼을 누르면 파일 선택하는 창이 나오게 되고 파일을 선택하면
파일명과 삭제 버튼이 priview 영역에 보이게 된다.

파일 삭제 버튼을 누를 경우 input form 태그의 값을 비워주는 형태로
작동하기 때문에 컨트롤러에 넘어갈 때는 빈값으로 넘어가기 때문에 빈값 처리가 필요하다.
