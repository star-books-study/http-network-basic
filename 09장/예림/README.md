# 9장. HTTP에 기능을 추가한 프로토콜

## 9.3 브라우저에서 양방향 통신을 하는 WebSocket

- HTTP 프로토콜을 사용하고 있는 이상, 병목현상을 해결할 수 없다.
- WebSocket은 새로운 프로토콜과 API에 의해 이 문제를 해결하기 위한 기술로서 개발됨.

### 9.3.1 WebSocket의 설계와 기능
- WebSocket은 웹 브라우저와 웹 서버를 위한 양방향 통신 규격으로 WebSocket 프로토콜을 IETF가 책정하고 WebSocket API를 W3C가 책정하고 있음.
- 주로 Ajax나 Comet에서 사용하는 XMLHttpRequest의 결점을 해결하기 위한 기술로서 개발이 진행되고 있음.

### 9.3.2 WebSocket 프로토콜
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
  HTTP/1.1 101 Switching Protocols
  Upgrade: websocket
  Connection: Upgrade
  Sec-WebSocket-Accept: s3pPLMBITiTxaQ9kYGzzhZRbK+xQo=
  Origin: http://example.com
  Sec-WebSocket-Protocol: chat
  ```
  - `Sec-WebSocket-Accept`에는 `Sec-WebSocket-Key`의 값에서 생성된 값이 저장됨
  - WebSocket 커넥션이 확립된 후에는, HTTP가 아닌, WebSocket 독자적인 데이터 프레임을 이용해 통신한다.
  
  <img width="450" alt="스크린샷 2024-07-20 오후 5 23 27" src="https://github.com/user-attachments/assets/333cec20-70ce-426c-bee8-a7f27d8c9996">

- **WebSocket API** : JavvaScript에서 WebSocket 프로토콜을 사용한 양방향 통신을 하기 위해서는 W3C에서 사양이 책정되어 있는 WebSocket 인터페이스를 사용해야 한다.
  ```javascript
  // WebSocket API를 사용해 50ms에 1번 데이터를 송신하는 예
  var socket = new WebSocket('ws://game.example.com:12010/updates');
  socket.onopen = function() {
    setInterval(function() {
      if(socket.bufferedAmount == 0)
        socket.send(getUpdateData());
    }, 50);
  };
  ```

  
