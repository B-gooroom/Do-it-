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
### HTTP method

#### #HTTP API를 만들어보자
 - API URI 설계
   - `리소스 식별`
   - 회원을 등록하고 수정하고 조회 -> '회원'이라는 개념이 리소스<br>
   -> `회원` 리소스를 URI 맵핑
   - 리소스 & 행위 분리
     - 리소스 = 회원
     - 행위 = 등록, 수정, 조회, 삭제

#### #HTTP method(resource => Representation)
 - GET : 리소스 조회
   - 서버ㅓ에 전달하고 싶은 데이터 query로 전달
   - 바디로 전달 가능하지만, 지원하지 않는 곳이 많음
 - POST : 요청 데이터 처리, 등록
   - 메시지 바디를 통해 서버로 요청
   - **대상 리소스가 리소스의 고유한 의미 쳬계에 따라 요청에 포함된 표현을 처리하도록 요청**
   - POST /order/{orderId}/start (컨트롤 URI)
 - PUT : 리소스 덮어쓰기, 해당 리소스가 없으면 생성
   - 클라이언트가 리소스 위치를 알고 URI 지정
 - PATCH : 리소스 부분 변경
   - 원하는 부분만 변경 가능
 - DELETE : 리소스 삭제

#### #HTTP method 속성
 - Safe
   - 호출해도 리소스를 변경하지 않음 -> get은 안전함
   - 해당 리소스의 변경만을 고려함
 - Idempotent(역동)
   - 한번 호출, 두번 호출, 100번 호출 해도 결과가 똑같음
     - get : 여러번 조회해도 최종결과는 같음
     - put : 결과를 대체, 같은 요청을 여러번 해도 최종결과는 같음
     - delete : 결과를 삭제, 같은 요청을 여러번 해도 최종 결과는 같음
     - post : 두번 호출하면 결과가 중복될 수 있음
   - 외부 요인(put, patch 등)으로 중간에 리소스가 변경되는 것까지는 고려하지 않음
 - Cacheable(캐시가능)
   - get, head, post, patch 캐시가능 -> 보통 get, head 정도만 캐시로 사용

---
### HTTP method use

#### #클라이언트에서 서버로 데이터 전송
 - 쿼리 파라미터를 통한 데이터 전송
 - 메시지 바디를 통한 데이터 전송
 - 4가지 상황
   - 정적 데이터 조회
     - <img width="600" alt="스크린샷 2023-04-17 오전 9 39 09" src="https://user-images.githubusercontent.com/79742210/233228784-4190f30d-483c-4ece-951b-a931962ca477.png">
     - 이미지, 정적 텍스트 문서
     - 조회는 GET 사용
     - 정적 데이터는 일반적으로 단순하게 조회 가능
   - 동적 데이터 조회
     - <img width="600" alt="스크린샷 2023-04-17 오전 9 45 24" src="https://user-images.githubusercontent.com/79742210/233228923-6deb99fd-b60d-4154-adc1-6135c1c4feb7.png">
     - 주로 검색, 게시판 목록, 정렬 필터
     - 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건
     - GET은 쿼리 파라미터 사용해서 데이터 전달
   - HTML Form을 통한 데이터 전송
     - POST
     - <img width="600" alt="스크린샷 2023-04-17 오전 10 04 02" src="https://user-images.githubusercontent.com/79742210/233229115-6bc4b808-7aaf-444c-917b-a3b11cbd7a40.png">
       - form의 내용을 body로 넘김(key=value, 쿼리 파라미터 형식)
       - 전송 데이터를 url encoding 처리
       - form 전송은 GET도 지원
     - multipart/form-data
     - <img width="600" alt="스크린샷 2023-04-17 오전 10 20 41" src="https://user-images.githubusercontent.com/79742210/233229808-eb29f8f2-1a63-4378-b8e3-6183eaf49975.png">
       - 파일 같이 바이너리 데이터 전송시 사용
       - 다른 종류의 여러 파일과 폼 내용을 함께 전송할 수 있음
 - HTTP API 데이터 전송
   - 백엔드 시스템 통신 - 서버 to 서버
   - 앱 클라이언트 - 아이폰, 안드로이드
   - 웹 클라이언트 - HTML에서 Form 전송 대신 스크립트를 통한 통신에 사용(ajax)
   - POST, PUT, PATCH - 메시지 바디를 통해 데이터 전송
   - GET - 조회, 쿼리 파라미터로 데이터 전달
   - Content-Type: application/json을 주로 사용(TEXT, XML, JSON 등)

#### #HTTP API 설계 에시
 - _HTTP API - 컬렉션 : post 기반 등록(ex.회원관리시스템)_
   - 회원 목록 /members -> GET
   - 회원 등록 /members/{id} -> POST
   - 회원 조회 /member/{id} -> GET(단건조회)
   - 회원 수정 /member/{id} -> PATCH, PUT, POST
   - 회원 삭제 /member/{id} -> DELETE
   - 특징
     - 클라이언트는 등록될 리소스의 URI를 모름
     - 서버가 새로 등록된 리소스 URI를 생성해줌<br>
     -> HTTP/1.1 201 Created Location: /members/100
     - 컬렉션
       - 서버가 관리하는 리소스 디렉토리
       - 서버가 리소스의 URI를 생헝하고 관리
       - 컬렉션 = /members

 - HTTP API - 스토어 : put 기반 등록(ex.파일관리시스템)
   - 파일 목록 /files -> GET
   - 파일 조회 /files/{filename} -> GET
   - 파일 등록 /files/{filename} -> PUT
   - 파일 삭제 /files/{filename} -> DELETE
   - 파일 대량 등록 /files -> POST
   - 특징
     - 클라이언트가 리소스 URI를 알고 있어야함
     - 클라이언트가 직접 리소스의 URI를 지정해줌
     - 스토어
       - 클라이언트가 관리하는 리소스 저장소
       - 클라이언트가 리소스의 URI를 알고 관리

 - HTML Form 사용
   - HTML Form은 GET, POST만 지원
   - 순수 HTML, HTML Form에 해당
   - 회원 목록 /members -> GET
   - 회원 등록 폼 /members/new -> GET
   - 회원 등록 /members/new, /members -> POST
   - 회원 조회 /member/{id} -> GET
   - 회원 수정 폼 /members/{id} -> GET
   - 회원 수정 /members/{id}/edit, /memers/{id} -> POST
   - 회원 삭제 /membmers/{id}/delete -> POST
   - 특징
     - HTML Form은 GET, POST만 지원
     - 컨트롤 URI
       - GET, POST만 지원하므로 제약이 있음
       - 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용
       - POST의 /new, /edit, /delte가 컨트롤 URI
       - HTTP 메서드로 해결하기 애매한 경우에 사용

 - 좋은 URI 설계 개념?
   - 문서(document)
     - 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
     - `ex. /members/100, /files/star.jpg`
   - 컬렉션(collection)
     - 서버가 관리하는 리소스 디렉토리
     - 서버가 리소스의 URI를 생성하고 관리
     - `ex. /members`
   - 스토어(store)
     - 클라이언트가 관리하는 자원 저장소
     - 클라이언트가 리소스의 URI를 알고 관리
     - `ex. /files`
   - 컨트롤러(controller), 컨트롤 URI
     - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
     - 동사를 직접 사용
     - `ex. /members/{id}/delete`

---
### HTTP 상태코드

#### #상태코드

