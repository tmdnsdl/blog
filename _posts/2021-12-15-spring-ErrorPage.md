---
title: "스프링에서 에러페이지 구현하기"
date: 2021-12-15
categories: Spring
---

### 스프링에서 에러페이지 구현하는 방법

---

기업의 프로젝트를 진행하는 경우 404나 SQL에러 등이 웹 페이지에 표시되면
보안 문제가 발생할 수 있기 때문에 에러페이지를 따로 만들어 에러나 예외 발생 시
에러 페이지를 보여주게 코드를 작성하게 된다.

이번에는 스프링 프레임워크를 사용한 프로젝트에서 보안을 위한 에러페이지 구현에 대해 알아보겠다.

---

**web.xml 설정**

```
<error-page>
	<exception-type>java.lang.Throwable</exception-type>
	<location>/error/throwable</location>
</error-page>
<error-page>
	<exception-type>java.lang.Exception</exception-type>
	<location>/error/exception</location>
</error-page>
<error-page>
	<exception-type>404</exception-type>
	<location>/error/404</location>
</error-page>
<error-page>
	<exception-type>403</exception-type>
	<location>/error/403</location>
</error-page>
<error-page>
	<exception-type>500</exception-type>
	<location>/error/500</location>
</error-page>
<error-page>
	<exception-type>503</exception-type>
	<location>/error/503</location>
</error-page>
<error-page>
	<exception-type>400</exception-type>
	<location>/error/400</location>
</error-page>
<error-page>
	<exception-type>405</exception-type>
	<location>/error/405</location>
</error-page>
```

web.xml에 해당하는 에러를 어떤 URL로 넘겨줄지에 대해 작성한다.

---

**Controller**

```
package com.raccoon.solution;

import javax.servlet.http.HttpServletRequest;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/error")
public class ErrorController {
	private static final Logger logger = LoggerFactory.getLogger(ErrorController.class);

	@RequestMapping("/throwable")
	public String throwable(HttpServletRequest request, Model model) {
		logger.info("throwable");
		pageErrorLog(request);
		model.addAttribute("msg", "예외가 발생하였습니다");
		return "common/errorPage";
	}

	@RequestMapping("/exception")
	public String exception(HttpServletRequest request, Model model) {
		logger.info("exception");
		pageErrorLog(request);
		model.addAttribute("msg", "예외가 발생하였습니다");
		return "common/errorPage";
	}

	@RequestMapping("/400")
	public String error400(HttpServletRequest request, Model model) {
		logger.info("400");
		pageErrorLog(request);
		model.addAttribute("msg", "잘못된 요청입니다");
		return "common/errorPage";
	}

	@RequestMapping("/403")
	public String error403(HttpServletRequest request, Model model) {
		logger.info("403");
		pageErrorLog(request);
		model.addAttribute("msg", "접근이 금지되었습니다");
		return "common/errorPage";
	}

	@RequestMapping("/404")
	public String error404(HttpServletRequest request, Model model) {
		logger.info("404");
		pageErrorLog(request);
		model.addAttribute("msg", "요청하신 페이지는 존재하지 않습니다");
		return "common/errorPage";
	}

	@RequestMapping("/405")
	public String error405(HttpServletRequest request, Model model) {
		logger.info("405");
		pageErrorLog(request);
		model.addAttribute("msg", "요청된 메소드가 허용되지 않습니다");
		return "common/errorPage";
	}

	@RequestMapping("/500")
	public String error500(HttpServletRequest request, Model model) {
		logger.info("500");
		pageErrorLog(request);
		model.addAttribute("msg", "서버에 오류가 발생하였습니다");
		return "common/errorPage";
	}

	@RequestMapping("/503")
	public String error503(HttpServletRequest request, Model model) {
		logger.info("503");
		pageErrorLog(request);
		model.addAttribute("msg", "서비스를 사용할 수 없습니다");
		return "common/errorPage";
	}

	private void pageErrorLog(HttpServletRequest request) {
		logger.info("status_code : " + request.getAttribute("javax.servlet.error.status_code"));
		logger.info("exception_type : " + request.getAttribute("javax.servlet.error.exception_type"));
		logger.info("message : " + request.getAttribute("javax.servlet.error.message"));
		logger.info("request_uri : " + request.getAttribute("javax.servlet.error.request_uri"));
		logger.info("exception : " + request.getAttribute("javax.servlet.error.exception"));
		logger.info("servlet_name : " + request.getAttribute("javax.servlet.error.servlet_name"));
	}

}
```

컨트롤러에 에러 로그처리와 각 에러에 해당하는 view로 보내주는 메시지를 작성한다.

---

**errorPage.jsp**

```
<!doctype html>
<html>
<head>
  <title>ErrorPage</title>
  <meta charset="utf-8">
</head>
<body>
  <div id="error-page">
    <div>
        <c:out value="${msg}"/>
        <p>관리자에게 문의 하세요</p>
    </div>
  </div>
</body>
</html>
```

view에서는 에러에 해당하는 메시지를 표시하여 준다.
