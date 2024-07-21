# 10장. 웹 콘텐츠에서 사용하는 기술

## 10.3 웹 애플리케이션
### 10.3.1 웹을 사용해서 기능을 제공하는 웹 애플리케이션
- 웹 애플리케이션은 동적 콘텐츠에 해당 (웹 서버 상의 프로그램이 HTML 등을 생성해서 반환)

### 10.3.2 웹 서버와 프로그램을 연계하는 CGI
- CGI(Common Gateway Interface) : 웹 서버가 클라이언트에서 받은 리퀘스트를 프로그램에 전달하기 위한 구조
- CGI에 의해 프로그램은 리퀘스트 내용에 맞게 HTML을 생성하는 등으로 동적 콘텐츠를 생성할 수 있음.
- CGI를 사용한 프로그램을 CGI 프로그램이라고 부르는데 Perl이나 PHP, Ruby, C언어 등의 프로그래밍 언어가 사용 중

![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/61/CGI_common_gateway_interface.svg/800px-CGI_common_gateway_interface.svg.png)

### 10.3.3 Java에서 보급된 서블릿
- 서블릿(Servlet) : 서버 상에 HTML 등의 동적 콘텐츠를 생성하기 위한 프로그램
- JavaEE(Java Enterprise Edition)의 일부로서 제공되고 있음
  - JavaEE : Java 프로그래밍 언어 사양의 하나로 엔터프라이즈 환경을 위한 Java
- CGI의 문제점을 해결하는 기술로서 Java와 함께 보급됨
- CGI는 리퀘스트마다 프로그램을 가동하기 때문에 대량 액세스가 있을 때 웹 서버 부하가 걸리게 되지만 서블릿에서는 웹 서버와 같은 프로세스 속에서 동작하기 때문에 비교적 부하를 적게 하여 동작시킬 수 있음.
- 서블릿의 실행 환경을 컨테이너 혹은 서블릿 컨테이너라고 부름

![](https://i0.wp.com/javaconceptoftheday.com/wp-content/uploads/2021/01/JavaServletArchitecture.png?fit=846%2C401&ssl=1)
