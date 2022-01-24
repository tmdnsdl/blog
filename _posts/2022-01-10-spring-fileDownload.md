---
title: "스프링 파일 다운/삭제 기능 구현하기"
date: 2022-01-10
categories: Spring
---

### 파일 다운로드 / 삭제 기능 구현

---

스프링에서 업로드 한 파일을 다운로드 / 삭제 하는 기능을 구현해보자.

---

**파일 다운로드**

```
@RequestMapping("/fileDownload")
 public String fileDownload(HttpServletResponse response, HttpServletRequest request) {

  String fileName = request.getParameter("file");

  if(fileName != null) {
   String filePath = "/download/"; // 파일 경로
   String originalFileName = "myfile"; // 다운로드 받을 파일명

   InputStream input = null;
   OutputStream output = null;

   File file = new File(filePath, fileName);
   try {
    input = new FileInputStream(file);
   } catch (FileNotFoundException e) {
    e.printStackTrace();
   }

   String client = request.getHeader("User-Agent");
   response.reset();
   response.setContentType("application/octet-stream");
   response.setHeader("Content-Description", "JSP Generated Data");

   // IE
   if(client.indexOf("MSIE") != -1) {
    try {
     response.setHeader("Content-Disposition", "attachment; filename=" + new String(originalFileName.getBytes("KSC5601"), "ISO8859_1"));
    } catch (UnsupportedEncodingException e) {
     // TODO Auto-generated catch block
     e.printStackTrace();
    }
   } else {
    try {
     originalFileName = new String(originalFileName.getBytes("utf-8"), "iso-8859-1");
    } catch (UnsupportedEncodingException e) {
     // TODO Auto-generated catch block
     e.printStackTrace();
    }
    response.setHeader("Content-Disposition", "attachment; filename=\"" + originalFileName + "\"");
    response.setHeader("Content-Type", "application/octet-stream; charset=utf-8");
   }
   response.setHeader("Content-Length", ""+file.length());

   try {
    output = response.getOutputStream();

    byte [] buffer = new byte[(int)file.length()];
    int readCount = 0;
    while((readCount = input.read(buffer)) > 0) {
     output.write(buffer,0,readCount);
    }

    input.close();
    output.close();

   }catch (IOException e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
   }
  } // file check
  return null;
 }
```

JSP 페이지에서 get, post방식으로 요청하는 것을 고려하여 작성되었다.
파일명이 원본 파일명과 다르게 설정되어 있다면 구분자 등으로 원본 파일명으로 다운로드 할 수 있게 설정해준다.
인터넷 익스플로러를 사용 중인 경우에도 문제가 없도록 코드를 작성하였다.

---

**파일 삭제**

```
public void deleteFile(String fileName) {
  if(fileName != null) {
   String filePath = "/upload/";
   String deleteFile = filePath + fileName;
   File file = new File(deleteFile);
   if(file.exists()) {
    file.delete();
   }
  }
 }
```

파일을 업로드 한 디렉토리에서 파일을 삭제하는 기능을 가진 메소드
필요한 페이지에서 수정 / 삭제 기능을 구현할 때 사용하면 된다.
