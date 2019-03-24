---
title: '[번역] Spring schema references 에는 버전을 정확히 명시하지 않는 것이 좋다.'
date: 2018-01-07 23:44:46
categories: translate
tags: [번역, Spring]
---

먼저 이 글은 <a href='https://howtodoinjava.com/spring/spring-core/do-not-specify-version-numbers-in-spring-schema-references/'>do-not-specify-version-numbers-in-spring-schema-references</a>을 번역한 글임을 밝혀둡니다.
혹시 문제가 될 경우 즉시 삭제 하겠습니다.

Spring schema references 에는 버전을 정확히 명시하지 않는 것이 좋다.

만약 당신이 스프링 프로젝트 기반에서 일을 하고 있다면 스프링 설정파일의 헤더 부분에 있는
스프링 모듈에 대한 schema references를 보았을 것이다.

스키마 레퍼런스에서 우리는 xml namespace와 버전 번호에 대한 얘기를 하고자 한다.

버전 번호를 명확하게 하는 것은 필수가 아니다, 그리고 당신은 그것을 뺄 수 있다.
여기 예제를 보면 사실, 버전은 제거 해야 한다.

스프링은 자동적으로 프로젝트에서 사용 가능한 가장 높은 버전의 모듈을 선택합니다.
또, 스프링 버전이 업데이트 되거나 프로젝트의 환경이 좋아지는 경우 새로운 기능을 위해 모든 xml 설정을 유지할 필요는 없습니다.

버전을 사용하지 않는 스프링 설정 파일의 사용 예제 

``` bash
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
       http://www.springframework.org/schema/context 
       http://www.springframework.org/schema/context/spring-context-3.0.xsd">

<!-- Other bean definitions-->

</beans>
```

이건 아래처럼 사용 될 수 있습니다.

``` bash
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd">
 
<!-- Other bean definitions-->
 
</beans>
```

의견을 덧붙이면..

개인적으로 스프링은 책으로 공부한 것보다 인터넷에서 찾아보며 공부한 시간이 더 많네요.
책에 이런 내용들이 담겨져 있다면 좋을 것 같다고 생각이 드네요.

기술적인 부분이라기 보다는 개발 편의성에 관련된 내용이라고 생각되지만,
그래도 모르는 것보다는 아는 것이 더 좋을 것 같아 이렇게 정리해 둡니다.

더불어 번역을 허락해주신 HowToDoInJava 의 주인이신 Lokesh Gupta 에게 감사 드립니다.
