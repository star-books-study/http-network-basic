# 제 2장. 간단한 프로토콜 HTTP
## 2.1. HTTP 는 클라이언트와 서버 간에 통신을 한다
- 텍스트, 이미지 같은 리소스를 필요하다고 요구하는 쪽이 클라이언트, 이러한 리소스를 제공하는 쪽이 서버이다
- HTTP 는 서버와 클라이언트의 역할을 명확히 구별하고 있다

## 2.2. 리퀘스트와 리스폰스를 교환하여 성립
```http
POST /lines/1 HTTP/1.1
Host: localhost:64521
Connection: keep-alive
Content-Type: ...
Content-Length: 16
```
- POST: `HTTP 메서드`로 어떤 동작을 요청하는지 식별한다.
- /lines/1 : URI로 서버에 요청하는 리소스를 나타낸다. (`Request URI`)
- HTTP/1.1 : 클라이언트 기능을 식별하기 위한 `HTTP 버전 번호`
- 나머지 부분 : 리퀘스트 헤더 필드
- 리퀘스트 메시지 = 메소드 + URI + 프로토콜 버전 + 옵션 리퀘스트 헤더 필드 + 엔티티
  - 엔티티 : ex) name=eunju&age=37