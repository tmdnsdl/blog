---
title: "Javascript 파일 확장자 유효성 검사"
date: 2022-01-04
categories: Javascript
---

### Javascript 파일 확장자 체크

---

보안으로 인해 파일 업로드 시 확장자를 제한하여 할 경우 확장자 검사하는 방법을 알아보자.

javascript에서 function으로 input의 file 태그에서 업로드 될 때 마다 확장자를 체크를 하여
업로드 하고 제한한 확장자의 경우 alert로 체크하는 방법이다.

다중 파일 업로드를 하는 경우도 고려하여 작성하였다.

---

**JSP**

```
<form action="fileUpload" method="post" enctype="multipart/form-data">
    <input type="file" name="file" id="file" multiple>
</form>
```

다중 파일 업로드 가능한 multiple 속성 추가

---

**Javascript**

```
    function checkFiles() {
  const inputFile = document.getElementById("file");
  const files = inputFile.files;
  let fileSize = 0;

  //파일 사이즈 확인
  for(let i=0; i<files.length;i++) {
   fileSize += files[i].size;
  }

  for(let i=0; i<files.length; i++) {
   // 파일 업로드 확장자 추가
   if(!/\.((jpg|jpeg|ppt|doc|docx|xls|xlsx|hwp|png|pptx|pdf|csv)$/i.test(files[i].name)) {
    alert('업로드 불가능한 확장자입니다.\n\n현재 파일: '+ files[i].name);
    inputFile.value = "";
    return false;
   } else if(fileSize > 209715200) {
    alert("파일은 200MB 이상 업로드 할 수 없습니다.");
    inputFile.value = "";
    return false;
   } else {
    return true;
   }
  }
 }
```

업로드 가능한 확장자만 등록하는 화이트리스트 방식으로 체크를 하여
원하는 확장자 업로드를 가능하게 한다.

---

**Controller**

```
    public boolean fileFilter(String str) {

  int fileIndex = str.lastIndexOf(".")+1;
  String fileName = str.substring(fileIndex);
  boolean result;

  if(fileName.equals("jpg") || fileName.equals("jpeg") || fileName.equals("pptx")
   || fileName.equals("pdf") || fileName.equals("ppt") || fileName.equals("doc")
   || fileName.equals("docx") || fileName.equals("xls") || fileName.equals("xlsx")
   || fileName.equals("hwp") || fileName.equals("png") || fileName.equals("csv")) {
   result = true;
  }
  else {
   result = false;
  }
  return result;
 }
```

Controller의 파일 처리 비지니스 로직에서 multipartFile의 getOriginalFileName()으로 얻은 값을
확장자 필터로 처리하여 result가 true일 경우에만 업로드를 처리하게 구현해야 보안 공격 등에 안전하다.
