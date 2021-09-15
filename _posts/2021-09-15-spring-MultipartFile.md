---
title: "스프링 서버에 파일 업로드하는 방법"
date: 2021-09-15
categories: Spring
---
### 스프링에서 서버에 파일 업로드하는 방법

---

스프링의 Multipart 지원 기능을 사용해 Multipart 형식으로 전송된 파라미터와 
파일 정보를 얻어 업로드가 가능하다.

MultipartResolver 설정

- Multipart 기능을 스프링에서 사용하려면 MultipartResolver를
스프링 설정 파일에 등록해주어야 한다.
- 스프링에서 기본으로 제공하는 MultipartResolver는 CommonsMultipartResolver이다.  
CommonsMultipartResolver는 CommonsFileUpload API를 이용하여 Multipart를 처리해준다

__servlet-context.xml에 MultipartResolver Bean을 등록__
```
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
	<property name="maxUploadSize" value="10485760"/>
	<property name="maxInMemorySize" value="10240"/>
	<property name="defaultEncoding" value="UTF-8"/>
</bean>
```

- DispatcherServlet은 이름이 "multipartResolver"인 Bean을 사용하기 때문에 
반드시 id를 multipartResolver로 지정해야 하며 다른 이름을 지정할 경우
MultipartResolver로 사용되지 않는다.

__pom.xml에 파일 업로드에 필요한 라이브러리를 등록__

```
<!-- 파일 업로드 -->
    <dependency>
        <groupId>commons-fileupload</groupId>
        <artifactId>commons-fileupload</artifactId>
        <version>1.2.2</version>
        <scope>runtime</scope>
    </dependency>       
        
    <dependency>
        <groupId>commons-io</groupId>
        <artifactId>commons-io</artifactId>
        <version>1.3.2</version>
        <scope>runtime</scope>
    </dependency>      
```

파일 업로드를 할 때는 form의 속성으로 enctype = multipart/form-data을 작성해야하고 
method가 post여야 한다.

- MultipartFile 인터페이스

org.springframework.web.MutipartFile 인터페이스는 업로드한 파일 및 파일데이터를
표현하기 위한 용도로 사용된다.

메소드 | 기능
--- | ---
getOriginalFilename() | 업로드한 파일의 이름을 리턴
byte[ ] getBytes() throws IOExcetion | 업로드한 파일 데이터를 리턴
transferTo(File dest) throws IOException | 업로드한 파일 데이터를 지정한  
파일에 저장한다