# 제 8장. 누가 액세스하고 있는지를 확인하는 인증
## 8.1. 인증이란?
- HTTP 에서 사용하는 인증 방법
  - BASIC 인증
  - DIGEST 인증
  - SSL 클라이언트 인증
  - 폼 베이스 인증

## 8.2. BASIC 인증
- 웹 서버와 대응하고 있는 클라이언트 사이에서 이뤄지는 인증 방식

### 8.2.1. BASIC 인증 수순
1. 클라이언트가 리퀘스트 송신
    ```http
    GET /private/ HTTP/1.1 
    Host: hackr.jp
    ```
2. BASIC 인증이 필요한 리소스가 있는 경우 서버는 상태코드 401 Authorization Required와 함께 **인증의 방식(BASIC), Request-URI의 보호 공간을 식별하기 위한 문자열(realm)을 WWW-Authenticate 헤더 필드에 포함시켜 리스폰스를 반환**
    ```http
    HTTP/1.1  401 Authorization Required
    Date:Mon, 19 Sep 2011 08:38:32 GMT
    Server: Apache/2.2.3 (Unix)
    WWW-Authenticate: Basic realm="Input Your ID and Password"
    ```
3. 상태 코드 401을 받은 클라이언트는 BASIC 인증을 위해 유저ID와 패스워드를 서버에 송신해야 함.<br>**송신하는 문자열은 유저ID와 패스워드를 콜론 ‘:’ 으로 연결한 문장을 Base64라 불리는 형식으로 인코드한 것.** <br>ex) ID가 guest이고 패스워드가 guest인 경우 guest:guest 문자열이 되는데 이를 Base64 인코드하면 Z3Vlc3Q6Z3Vlc3Q= 이 된다. 이 문자열을 Authorization 헤더 필드에 포함해서 리퀘스트를 송신
    ```http
    Get /private/ HTTP/1.1
    Host: hacker.jp
    Authorization: Basic Z3Vlc3Q6Z3Vlc3Q=
    ```
4. Authorization 헤더 필드를 포함한 리퀘스트를 수신한 서버는 인증 정보가 정확한지 여부를 판단. <br> 인증 정보가 정확하면 Request-URI 리소스를 포함한 리스폰스를 반환
    ```http
    HTTP/1.1  200 OK
    Date:Mon, 19 Sep 2011 08:38:35 GMT
    Server: Apache/2.2.3 (Unix)
    ```

- BASIC 인증에서는 **Base64 라는 인코딩 형식을 사용하고 있지만, 암호화는 아니기 때문에 아무런 부가정보 없이도 복호화할 수 있다**
- HTTPS 등에서 암호화되지 않은 통신 경로 상에서 BASIC 인증을 해서 도청된 경우, 복호화된 유저 아이디와 패스워드를 빼앗길 가능성이 있다
- 한번 BASIC 인증을 하면, 일반 브라우저에서는 로그아웃 할 수 없다
- BASIC 인증은 사용상의 문제와 많은 웹사이트에서 요구되는 보안 등급에는 미치치 못한다