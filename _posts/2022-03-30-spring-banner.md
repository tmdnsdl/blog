---
title: "스프링 부트 배너 구현하기"
date: 2022-03-30
categories: Spring
---

### Spring boot banner

---

스프링 부트에서 서버가 기동될때 나오는 배너인 아스키 아트를
내가 원하는 배너로 구현하는 방법에 대해 알아보자.

---

**banner.txt**

```
${AnsiColor.BRIGHT_BLUE}████████████████████████████████████████████████████████████████████████████████
${AnsiColor.BRIGHT_BLUE}████████████████████████████████████████████████████████████████████████████████
${AnsiColor.RED}██████████████████${AnsiColor.BRIGHT_BLUE}████████████████${AnsiColor.BLACK}██████████████████████████████${AnsiColor.BRIGHT_BLUE}████████████████
${AnsiColor.RED}████████████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████████████████████████████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██████████████
${AnsiColor.BRIGHT_RED}████${AnsiColor.RED}██████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.MAGENTA}██████████████████████${AnsiColor.WHITE}██████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████████████
${AnsiColor.BRIGHT_RED}██████████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}████${AnsiColor.MAGENTA}████████████████${AnsiColor.BLACK}████${AnsiColor.MAGENTA}██████${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██${AnsiColor.BLACK}████${AnsiColor.BRIGHT_BLUE}██████
${AnsiColor.BRIGHT_RED}██████████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.MAGENTA}████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.MAGENTA}██████${AnsiColor.WHITE}██${AnsiColor.BLACK}████${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████
${AnsiColor.BRIGHT_YELLOW}██████████████████${AnsiColor.BRIGHT_RED}████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.MAGENTA}████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.MAGENTA}██████${AnsiColor.WHITE}██${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████
${AnsiColor.BRIGHT_YELLOW}██████████████████████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_YELLOW}██████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.MAGENTA}████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.BLACK}████████${AnsiColor.WHITE}████████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████
${AnsiColor.BRIGHT_YELLOW}████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.BLACK}██${AnsiColor.BRIGHT_YELLOW}████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.MAGENTA}████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████████████████████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████
${AnsiColor.BRIGHT_GREEN}██████████████████${AnsiColor.BRIGHT_YELLOW}██${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.BLACK}████████${AnsiColor.WHITE}██${AnsiColor.MAGENTA}██████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████████████████████████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██
${AnsiColor.BRIGHT_GREEN}██████████████████████${AnsiColor.WHITE}████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.MAGENTA}██████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.BRIGHT_YELLOW}██${AnsiColor.WHITE}██████████${AnsiColor.BRIGHT_YELLOW}██${AnsiColor.BLACK}██${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██
${AnsiColor.BRIGHT_GREEN}██████████████████████${AnsiColor.BLACK}████${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.MAGENTA}██████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.BLACK}████${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██
${AnsiColor.BLUE}██████████████████${AnsiColor.BRIGHT_GREEN}████████${AnsiColor.BLACK}██████${AnsiColor.WHITE}██${AnsiColor.MAGENTA}██████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.MAGENTA}████${AnsiColor.WHITE}████████████████${AnsiColor.MAGENTA}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██
${AnsiColor.BLUE}██████████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}████${AnsiColor.MAGENTA}██████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.BLACK}████████████${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████
${AnsiColor.BRIGHT_BLUE}██████████████████${AnsiColor.BLUE}████${AnsiColor.BLUE}██████${AnsiColor.BLACK}████${AnsiColor.WHITE}██████${AnsiColor.MAGENTA}██████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████████████████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██████
${AnsiColor.BRIGHT_BLUE}██████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██${AnsiColor.BLACK}████${AnsiColor.WHITE}████████████████████${AnsiColor.BLACK}██████████████████${AnsiColor.BRIGHT_BLUE}████████
${AnsiColor.BRIGHT_BLUE}████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}██████${AnsiColor.BLACK}████████████████████████████████${AnsiColor.WHITE}██${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████████████
${AnsiColor.BRIGHT_BLUE}████████████████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}██${AnsiColor.BLACK}██${AnsiColor.WHITE}████${AnsiColor.BRIGHT_BLUE}████████████${AnsiColor.BLACK}██${AnsiColor.WHITE}████${AnsiColor.BLACK}████${AnsiColor.WHITE}████${AnsiColor.BLACK}██${AnsiColor.BRIGHT_BLUE}████████████
${AnsiColor.BRIGHT_BLUE}████████████████████████${AnsiColor.BLACK}██████${AnsiColor.BRIGHT_BLUE}████${AnsiColor.BLACK}██████${AnsiColor.BRIGHT_BLUE}████████████${AnsiColor.BLACK}██████${AnsiColor.BRIGHT_BLUE}████${AnsiColor.BLACK}██████${AnsiColor.BRIGHT_BLUE}████████████
████████████████████████████████████████████████████████████████████████████████
${AnsiColor.BRIGHT_BLUE}:: Meow :: Running Spring Boot ${spring-boot.version} :: \ö/${AnsiColor.DEFAULT}
```

<https://github.com/snicoll/spring-boot-4tw-uni/blob/main/spring-boot-4tw-web/src/main/resources/banner.txt>

위 링크의 custom 배너를 사용하였다.
spring boot 프로젝트의 resources에 banner.txt 파일을 만들고 코드를 적용시키면
서버가 기동될때 나오는 배너가 변경이 된다.
