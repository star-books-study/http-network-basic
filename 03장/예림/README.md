# 3장. HTTP 정보는 HTTP 메시지에 있다
## 3.1 HTTP 메시지
- HTTP 메시지 : 복수 행의 데이터로 구성된 텍스트 문자열
- HTTP 메시지는 크게 구분하면 메시지 헤더와 메시지 바디로 구성되어 있고, 최초에 나타나는 개행 문자(CR+LF)로 메시지 헤더와 바디를 구분

> 메시지 바디가 항상 존재한다고 할 수는 없다

![](https://blog.kakaocdn.net/dn/bviYxW/btrHSA7bZEf/EnsoTYRPaBd7GxMMiZGCrk/img.png)

- **메시지 헤더** : 서버와 클라이언트가 꼭 처리해야 하는 리퀘스트와 리스폰스 내용과 속성 등

- **CR+LF** : CR(Carriege return : 16진수 0x0d)와 LF(line feed : 16진수 0x0a)

- **메시지 바디** : 꼭 전송되는 데이터 그 자체

## 3.2 리퀘스트 메시지와 리스폰스 메시지의 구조

![](https://velog.velcdn.com/images%2Fanhesu11%2Fpost%2Ff9934c03-a615-41ff-8862-219629fb0aee%2Fimage.png)

- **리퀘스트 라인** : 리퀘스트에 사용하는 메서드와 리퀘스트 URI와 사용하는 HTTP 버전 포함
- **상태 라인** : 리스폰스 결과를 나타내는 상태 코드와 설명, 사용하는 HTTP 버전
- **헤더 필드** : 리퀘스트와 리스폰스의 여러 조건과 속성 등을 나타내는 각종 헤더 필드 포함
  - 일반 헤더 필드, 리퀘스트 헤더 힐드, 리스폰스 헤더 필드, 렌티티 헤더 필드 등 4종류가 있다.
- 그 외 : HTTP의 RFC에는 없는 헤더 필드(쿠키 등) 포함

![](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages/http_request_headers3.png)
![](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages/http_response_headers3.png)

## 3.3 인코딩으로 전송 효율을 높이다
