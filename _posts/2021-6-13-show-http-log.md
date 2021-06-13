---
layout: post
title: HTTP 요청 메시지 로그로 확인하기 
---

- application.properties 파일에 다음 설정 추가
```
  logging.level.org.apache.coyote.http11=debug
```  
- http 요청 정보를 확인할 수 있다. 
- 운영서버에서 적용하면 성능저하가 발생할 수 있으므로 개발 단계에서만 사용