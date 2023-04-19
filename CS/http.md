## HTTP 웹 기본 지식

### 인터넷 네트워크

#### #인터넷 통신
<img width="600" alt="스크린샷 2023-03-24 오후 1 17 10" src="https://user-images.githubusercontent.com/79742210/232988601-6f2a1746-8c5e-4353-ad46-d24c256f1c55.png">

#### #IP(Internet Protocol)
 - 지정한 IP 주소에 데이터 전달
 - 단위: `packet`(package + bucket)
 - <img width="600" alt="스크린샷 2023-03-24 오후 1 17 36" src="https://user-images.githubusercontent.com/79742210/232991547-f0c67c80-fde3-44e8-9a4a-18c8894b40ee.png">
 - `출발지 IP, 목적지 IP, data`
 - 한계
   - 비연결성 - 패킷의 대상이 없거나, 불능 상태여도 패킷이 전송됨(우편물 보내듯이)
   - 비신뢰성 - 패킷이 중간에 사라지거나, 요청 순서대로 오지 않는다면?
   - 프로그램 구분(중독성) - 같은 IP를 사용하는 서버에서 통신하는 app이 둘 이상일 때?

#### #TCP
 - `출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증정보`
 - 인터넷 프로토콜 스택 4계층
<table>
    <tr>
        <td>애플리케이션 계층 - HTTP, FTP</td>
    </tr>
    <tr>
        <td>전송 계층 - TCP, UDP</td>
    </tr>
    <tr>
        <td>인터텟 계층 - IP</td>
    </tr>
    <tr>
        <td>네트워크 인터페이스 계층</td>
    </tr>
</table>
* <img width="300" alt="스크린샷 2023-03-24 오후 2 44 16" src="https://user-images.githubusercontent.com/79742210/232994731-90d1c364-3914-45bc-a1be-d6b380e52a06.png">
* <img width="600" alt="스크린샷 2023-03-24 오후 2 44 49" src="https://user-images.githubusercontent.com/79742210/232994906-ea34c7cb-025c-43b0-ac39-05d692f53d86.png">

  1. 프로그램이 `안녕!` 메시지 생성
  2. Socket 라이브러리를 통해 전달
  3. TCP 정보 생성, 메시지 데이터 포함
  4. IP 패킷 생성, TCP 데이터 포함
 - 특징
  - 연결지향 - `TCP 3 way handshake` (연결이 되어있는지 확인하고 전송)
    - syn: 접속요청 & ack: 요청수락을 3번 주고 받음
    - <img width="600" alt="스크린샷 2023-03-24 오후 2 53 52" src="https://user-images.githubusercontent.com/79742210/233004180-22062985-7659-44ca-9153-766b29ecfb68.png">
  - 데이터 전달 보증(중간 누락시 알림)
    - 데이터 전송 & 데이터 받았음 송수진
  - 순서 보장
    - 1-2-3 순서대로 도착하지 않으면 클라이언트에게 다시 요청

#### #UDP(User Datagram Protocol)
 - `IP + PORT + checksum` 정도만 
 - 하얀 도화지
 - http 3에서 udp 프로토콜을 적용함(단순하고 빠른 장점)

#### #PORT
 - 같은 IP 안에서 프로세스 구분
 - <img width="600" alt="스크린샷 2023-03-31 오후 1 53 09" src="https://user-images.githubusercontent.com/79742210/233005142-0e18343e-fa81-4abf-94f0-06a52a6b03b7.png">
 - IP - 아파트 동, PORT - 아파트 호수
   - FTP - 20, 21
   - TELNET - 23
   - HTTP - 80
   - HTTPs - 443

#### #DNS(Domain Name Service)
 - 도메인 명을 IP주소로 변환
 - IP 주소가 바뀌더라도, 접근이 가능함
 - <img width="600" alt="스크린샷 2023-03-31 오후 3 33 58" src="https://user-images.githubusercontent.com/79742210/233005543-ccc5e345-614d-41d9-8f49-bbe1d96bc737.png">

---
### URI

#### #URI(Uniform Resource Identifier)
 - 소스 식별을 위한 통일된 방식
  - 로케이터 Locator -> ex. 집주소
  - 이르 Name -> ex. 정새미
 - URN 이름만으로는 실제 리소스를 찾을 수 있는 방법x
 - <img width="600" alt="스크린샷 2023-03-31 오후 3 44 50" src="https://user-images.githubusercontent.com/79742210/233008102-8c84d278-f384-4180-acb3-c107fe4a3552.png">
 - URL 문법
 ```Javascript
scheme://[userinfo@]host[:port][/path][?query][#fragment]
 ```
  - scheme: 주로 프로토콜 - http, https, ftp
  - userinfo: 사용자정보 포함해서 인증(거의 사용하지 않음)
  - host: 도메인 명 IP주소 직접 사용 가능
  - port: 접속 포트, 일반적으로 생략(http = 80, https = 443)
  - path: 리소스 경로, 계층적 구조
  - query: key=value 형태(?로 시작, &으로 추가 가능) - query parameter || query string
  - fragment: html 내부 북마크 사용, 서버 전송 x

---
### HTTP

#### #모든 것이 HTTP
 - HTTP(Hyper Text Transfer Protocol)
   - 거의 모든 형태의 데이터 전송 가능(HTML, text, image 등등)
   - 서버간 데이터 주고 받을 때에도 사용
 - HTTP 1.1이 중요(주로 사용)
   - TCP: HTTP/1.1, HTTP/2
   - UCP: HTTP/3
 - 특징
   - 클라이언트 서버 구조
   - 무상태 프로토콜(스테이스리스), 비연결성
    - HTTP 메시지
    - 단순함, 확장
 
#### #클라이언트 서버 구조
 - Request & Response 구조
 -  <img width="600" alt="스크린샷 2023-04-03 오전 11 41 07" src="https://user-images.githubusercontent.com/79742210/233011708-9aa17475-2254-4bc2-8a22-441c9d708506.png">
 - client/ server 구조 분리
   - client: serve에 요청, 응답 대기
   - server: client 요청에 대한 결과 만들어서 응답
 
#### #Stateful, Stateless(무상태 프로토콜)
 - Stateful: 중간에 `클라이언트 <-> 서버` 바뀌면 안됨
 - Stateless: `응답 서버`를 쉽게 바꿀 수 있음
 - 장점
   - 통신 중간에 서버측 장애가 나더라도 `Stateless` 상태 라면 2번째 서버가 응답해 줄 수 있음
   - <img width="600" alt="스크린샷 2023-04-03 오후 2 01 41" src="https://user-images.githubusercontent.com/79742210/233012766-9e0b365b-39d3-4372-b16a-d6990de75c9d.png">
   - 스케일 아웃(수평 확장 유리) 설계에 유리
 - 한계
   - 상태 유지(로그인)을 해야할 경우<br>
   -> 일반적으로 쿠키와 세션을 사용해서 상태유지 -> 최소한으로 사용해야함
   - 데이터를 많이 보내게 됨

#### #비 연결성(connectionless)
 - 장점
   - 연결을 유지하지 않는 모델
     - TCP/IP 연결 > 요청 > 응답 > TCP/IP 연결 종료
     - <img width="600" alt="스크린샷 2023-04-03 오후 2 23 19" src="https://user-images.githubusercontent.com/79742210/233013511-0cf8d0a7-6183-4c38-be1c-4603aa72128f.png">
   - 초 단위 이하의 빠른 속도로 응답
   - 서버는 연결 유지 x, 최소한의 지원만 사용하여 서버 유지
 - 단점
   - TCP/IP 연결을 새로 맺어야 함
   - HTML, Javascript, css 이미지 등 수많은 자원이 함께 다운로드
   - HTTP 지속 연결(Persistent Connections)로 문제 해결
   - <img width="600" alt="스크린샷 2023-04-03 오후 2 45 32" src="https://user-images.githubusercontent.com/79742210/233014172-d76a9b85-ea4c-42f0-aaa1-c3a82fd35cd1.png">
 - 어려운 업무?
   - 같은 시간에 발생하는 대용량 트래픽(ex. 선착순 이벤트 ,명절 KTX 예약, 수강신청 등)

#### #HTTP 메시지
 - HTTP 메시지 구조
 - <img width="400" alt="스크린샷 2023-04-03 오후 3 07 28" src="https://user-images.githubusercontent.com/79742210/233014551-3c911cb0-d681-4532-b5bd-d0c33dddcbc9.png">
 - Request & Response
 - <img width="600" alt="스크린샷 2023-04-03 오후 3 35 11" src="https://user-images.githubusercontent.com/79742210/233014789-c235d7ec-4860-4c5b-b54b-def67218ab42.png">

---
