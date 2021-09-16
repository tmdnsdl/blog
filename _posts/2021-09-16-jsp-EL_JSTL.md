---
title: "EL / JSTL"
date: 2021-09-16
categories: JSP
---

### [JSP] EL / JSTL 코드 예제

---

JSP 파일에 자바 코드를 스크립트릿이 아닌 EL (Expression Language) 과 JSTL (Jsp Standard Tag Library)를 이용해 작성하는 예제를 확인해보자

* 기본 설정

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
```

* eq / ne

```
<!-- param.code : A,B,C,D -->
<c:if test="${param.code eq 'A'}">A</c:if>
<c:if test="${param.code eq 'B'}">B</c:if>
<c:if test="${param.code eq 'C'}">C</c:if>
<c:if test="${!(param.code eq 'A' || param.code=='B' || param.code eq 'C')}">D</c:if>
<c:if test="${(param.code ne 'A' || param.code!='B' || param.code ne 'C')}">D</c:if>
```

* varStatus

```
<!-- varStatus = "사용자 지정 변수" var의 값 상태를 확인 
	index는 begin과 step의 값에 영향을 받음 -->
<c:forEach var="cnt" begin="1" end="10" step="2" varStatus="a"> 
	${cnt }/ ${a.index } / ${a.count } / ${a.first } / ${a.last } / ${a.begin } / ${a.end }
</c:forEach>
```

* forTokens

```
<c:set var="list" value="ab/cd*ef/g/h"/>
<c:forTokens var="token" items="${list }" delims="/*" varStatus="status">
	${status.count } : <c:out value="${token }"/>
</c:forTokens>
```

* functions

```
<c:set var="str1" value="      Functions <태그>를 사용합니다." />
<c:set var="str2" value="사용" /> 
<c:set var="tokens" value="1,2,3,4,5,6,7,8,9,10" />

length(str1) = ${fn:length(str1)} 
toUpperCase(str1) = "${fn:toUpperCase(str1)}"
toLowerCase(str1) = "${fn:toLowerCase(str1)}"
substring(str1, 7, 10) = "${fn:substring(str1, 7, 10)}" 
<!-- 0부터 시작 / 7~10 사이의 문자열 리턴 -->
substringAfter(str1, str2) = "${fn:substringAfter(str1, str2)}"
<!-- str1에서 str2가 해당하는 부분 뒤의 문자열 리턴 -->  
substringBefore(str1, str2) = "${fn:substringBefore(str1, str2)}"
<!-- str1에서 str2가 해당하는 부분 앞의 문자열 리턴 -->  
trim(str1) = "${fn:trim(str1)}" 
length(trim(str1)) = "${fn:length(fn:trim(str1))}" 
replace(str1, src, dest) = "${fn:replace(str1, " ", "-")}"
<!-- str1에서 src가 해당하는 부분을 dest로 변경 -->  
indexOf(str1, str2) = "${fn:indexOf(str1, str2)}" 
startsWith(str1, str2) = "${fn:startsWith(str1, 'Fun')}" 
endsWith(str1, str2) = "${fn:endsWith(str1, "합니다.")}"
contains(str1, str2) = "${fn:contains(str1, str2)}" 
containsIgnoreCase(str1, str2) = "${fn:containsIgnoreCase(str1, str2)}"
split(tokens, '') = "${fn:split(tokens, ',')}"
```

* fmt:format

```
<fmt:formatNumber value="99999" type="currency" currencySymbol="원"/>
<fmt:formatNumber value="99999" type="percent"/>

<fmt:formatDate value="${date()}" type="both" dateStyle="full" timeStyle="full"/>
<fmt:formatDate value="${date()}" type="both" dateStyle="medium" timeStyle="medium"/>
<fmt:formatDate value="${date()}" type="both" dateStyle="short" timeStyle="short"/>
<fmt:formatDate value="${date()}" type="date" dateStyle="full"/>
<fmt:formatDate value="${date()}" type="time" timeStyle="full"/>
<fmt:formatDate value="${date()}" pattern="yyyy-MM-dd HH:mm:ss"/>

<fmt:parseDate var="day" value="${bean.day}" pattern="yyyy-MM-dd"/>
<fmt:formatDate value="${day}" pattern="yyyy-MM-dd"/>
```