---
title: "Spring boot Ehcache"
date: 2017-09-11
draft: true
tags: [spring-boot, ehcache]
---

관리자 기능 프로젝트를 주로 하다보니 특별히 캐쉬를 적용해야 하는 상황이 없었다. 그만큼 사용자의 요청이 빈번하지 않아서 이기도 하지만 모니터링 시스템에서는 캐쉬 적용이 오히려 죽은정보를 표현할 수 있는 cache 배제해야 겠다.

일단 캐쉬 적용 방법은 spring-boot 에서는 정말로 간단하다.

라이브러리 추가

ehcache.xml 추가 및 설정

application 설정에 ehcache 추가

어노테이션 추가

이러면 캐쉬 사용할 수 있는 환경 설정은 끝이다.

이보다 더 중요한것은 어디에 적용할 것인가이다.

적용대상
공통코드
조회가 빈번한곳 
과거 통계 날짜기준

고려사항
와스 메모리 부하 고려한 설정
 - 엘리멘트수
 - timeIdel
 - 사용하는시간
 - 파일사용여부

서버 이중화시 분산캐쉬 적용해야됨

http://javacan.tistory.com/entry/133



cache 설정의 적정 주기는 얼제일까? 1시간? 10분? 1분?
