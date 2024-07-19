# 9장. HTTP에 기능을 추가한 프로토콜

## 9.3 브라우저에서 양방향 통신을 하는 WebSocket

- HTTP 프로토콜을 사용하고 있는 이상, 병목현상을 해결할 수 없다.
- WebSocket은 새로운 프로토콜과 API에 의해 이 문제를 해결하기 위한 기술로서 개발됨.

### 9.3.1 WebSocket의 설계와 기능
- WebSocket은 웹 브라우저와 웹 서버를 위한 양방향 통신 규격으로 WebSocket 프로토콜을 IETF가 책정하고 WebSocket API를 W3C가 책정하고 있음.
- 주로 Ajax나 Comet에서 사용하는 XMLHttpRequest의 결점을 해결하기 위한 기술로서 개발이 진행되고 있음.

### 6.3.2 WebSocket 프로토콜
- WebSocket은 **웹 서버와 클라이언트가 한 번 접속을 확립하면 그 뒤의 통신을 모두 전용 프로토콜로 하는 방식**
- JSON, XML, HTML이나 이미지 등 임의 형식의 데이터를 보내게 됨.

- HTTP에 의한 접속의 출발점이 클라이언트에 있다는 것에는 변함이 없지만 한 번 접속을 확립하면 WebSocket을 사용하여 서버와 클라이언트 어느 쪽에서도 송신을 할 수 있게 된다.

#### 주요 특징
- **서버 푸시 기능** : 서버에서 클라이언트에 데이터를 푸시하는 기능. 그래서 서버는 클라이언트의 리퀘스트를 기다리지 않고 데이터를 보낼 수 있음.
- **통신량의 삭감** : HTTP에 비해 자주 접속을 하는 오버헤드가 적어지고, 헤더의 사이즈도 작음 ➡️ 통신량 삭감
  - WebSocket으로 통신을 하려면 한 번 HTTP에 접속을 확립하고, WebSocket에 의해 통신을 하기 위해 핸드쉐이크 절차를 밟을 필요가 있음.
- **핸드쉐이크 / 리퀘스트** : WebSocket으로 통신을 하려면 HTTP의 `Upgrade` 헤더 필드를 사용해서 프로토콜을 변경하는 것으로 핸드쉐이크 실시
  ```
  GET /chat HTTP/1.1
  Host: server.example.com
  Upgrade: websocket
  Connection: Upgrade
  Sec-WebSocket-Key: dGhlllHNhbXBsZSBub25jZQ==
  Origin: http://example.com
  Sec-WebSocket-Protocol: chat, superchat
  Sec-WebSocket-Version: 13
  ```
  - `Sec-WebSocket-Key`에는 핸드쉐이크에 필요한 키 저장
  - `Sec-WebSocket-Protocol`에는 사용하는 서브 프로토콜 저장 (서브 프로토콜은 WebSocket 프로토콜에 의한 커넥션을 여러 개로 구분하고 싶을 때 이름을 붙여서 정의_
- **핸드쉐이크 / 리스폰스** : 앞선 리퀘스트에 대한 리스폰스는 상태 코드 [101 Switching Protocols]로 반환된다.
  ```
  ```
  
