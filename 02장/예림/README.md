# 2장. 간단한 프로토콜 HTTP
## HTTP는 클라이언트와 서버 간에 통신을 한다
- HTTP는 클라이언트와 서버의 역할을 명확하게 구별하고 있다.

## 리퀘스트와 리스폰스를 교환하여 성립
- 서버 측은 리퀘스트를 수신하지 않으면 리스폰스가 발생하는 경우는 없다.

### 리퀘스트
- 아래는 클라이언트 측으로부터 HTTP 서버에 송신된 리퀘스트 내용이다.
  ```
  GET /index.html HTTP/1.1
  Host: www.hackr.ip
  ```
  - GET : 메서드
  - /index.html : 리소스
  - HTTP/1.1 : 클라이언트의 기능을 식별하기 위한 HTTP 버전 번호
- 리퀘스트 메시지는 메서드, URI, 프로토콜 버전, 옵션 리퀘스트 헤더 필드와 엔티티로 구성
  ![image](https://github.com/star-books-coffee/http-network-basic/assets/101961939/7eeb65c4-9e31-42f2-9cc6-39c5e613a23a)

### 리스폰스
```
