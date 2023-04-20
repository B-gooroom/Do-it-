
## HTTP 웹 기본 지식
https://b-gooroom.notion.site/HTTP-0f94352250d642358961fd889834ce70

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
 - 클라이언트가 보낸 요청의 처리상태를 응답
 - 1xx (Informational) : 요청이 수신되어 처리중
 - 2xx (Successful) : 요청 정상 처리
   - 200 - OK
   - 201 - Created
   - 202 - Accepted (배치 처리에서 사용)
   - 204 - No Content (서버가 요청을 성공적으로 수행했지만, 응답보낼 컴텐츠가 없음)
 - 3xx (Redirection) : 요청을 완료하려면 추가 행동이 필요 -> 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동
   - <img width="600" alt="스크린샷 2023-04-18 오전 10 47 01" src="https://user-images.githubusercontent.com/79742210/233238443-d7139663-ee58-4f99-aaa9-fa80faa592aa.png">
   - 300 - Multiple Choices
   - 301 - Moved Permanently
   - 302 - Found
   - 303 - See Other
   - 304 - Not Modified
   - 307 - Temporary Redirect
   - 308 - Permanent Redirect
   - 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동
     - 301 - 리다이렉트시 요청 메서드가 GET으로 변함, 본문이 제거될 수 있음
     - 308 - 리다이렉트시 요청 메서드와 본문 유지
   - 일시 리다이렉션 - 일시적인 변경 (3개의 기능은 같음)
     - 302 - 리다이렉트시 요청 메서드가 GET으로 변함, 본문이 제거될 수 있음(기본값)
     - 307 - 리다이렉트시 요청 메서드와 본문 유지(메서드를 변경하면 안됨)
     - 303 - 리다이렉트시 요청 메서드가 GET으로 변경
     - ex - PRG(Post, Redirect, Get)
       - <img width="600" alt="스크린샷 2023-04-18 오전 11 28 04" src="https://user-images.githubusercontent.com/79742210/233239179-2cbe0de6-e3ef-4c56-8818-24ab234ffff6.png">
   - 특수 리다이렉션 - 결과 대신 캐시를 사용
     - 304 - 캐시를 목적으로 사용
 - 4xx (Client Error) : 클라이언트 오류, 잘못된 문법 등으로 서버가 요청을 수행할 수 없음
   - 400 Bad Request
     - 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음
     - 요청구문, 메시지 오류 등
   - 401 Unauthorized
     - 클라이언트가 해당 리소스에 대한 인증이 필요함
   - 403 Forbidden
     - 서버가 요청을 이해했지만 승일을 거부함
     - 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
   - 404 Not Found
     - 요청 리소스를 찾을 수 없음
 - 5xx (Server Error) : 서버 오류, 서버가 정상 요청을 처리하지 못함
   - 500 Internal Server Error
     - 서버 내부 문제로 오류 발생
   - 503 Service Unavailiable
     - 서비스 이용 불가
     - 서버가 일시적인 과부하 또는 예정된 작업을 요청을 처리할 수 없음

---
### Header

#### #일반헤더
 - HTTP 전송에 필요한 모든 부가정보
 - HTTP 표준
   - RFC2616 (과거) - 1999년
   - RFC7230 ~ 7235 - 2014년
     - message body를 통해 표현 데이터 전달
     - 메시지 본문 = payload
     - 표현은 요청이나 응답에서 전달할 실제 데이터
     - 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공

#### #표현
 - Content-Type : 표현 데이터의 형식
   - body에 들어가는 내용
   - text/html, application/json, image/png
 - Content-Encoding : 표현 데이터의 압축 방식
   - 표현 데이터를 압축하기 위해 사용
   - gzip, deflate, identitiy(압축x)
 - Content-Language : 표현 데이터의 자연 언어
   - 표현 데이터의 자연언어를 표현
   - ko, en, en-US
 - Content-Length : 표현 데이터으 ㅣ길이
   - 표현 데이터의 길이
   - byte 단위

#### #협상(콘텐츠 네고시에이션)
 - Accept : 클라이언트가 선호하는 미디어 타입 전달
 - Accept-Charset : 클라이언트가  선호하는 문자 인코딩
 - Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
 - Accept-Language : 클라이언트가 선호하는 언어
 - <img width="600" alt="스크린샷 2023-04-18 오후 2 06 24" src="https://user-images.githubusercontent.com/79742210/233241658-3bfdb2f5-a1f5-4419-b190-6c75233e688d.png">
 - 협상과 우선순위 1
   - Quality Values(q) 값 사용
   - 0 ~ 1, 클수록 높은 우선순위
   - 생략한다면 1로 인식
   ```shell
   ? GET /event
   Accept-Language : ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
   ```
   - 위와 같은 Accept-Language를 가졌을 때? 아래와 같이 볼 수 있음
   ```shell
   ko-KR; (q=1) / en-US; q=0.8 / en; q=0.7
   ```
   - ko-KR > en-US > en
 - 협상과 우선순위 2
   - 구체적인 것이 우선
   ```shell
   ? GET /event
   Accept: text/*, text/plain, text/plain;format-flowed, */*
   ```
   - text/plain;format=flowed > text/plain > text/* > */*
 - 협상과 우선순위 3
   - 구체적인 것을 기준을 미디어 타입을 맞춤
   ```shell
   ? GET /event
   text/*;q=0.3, text/html;q=0.7, text/html;level=1,
   text/html;level=2;q=0.4, */*;q=0.5
   ```
<table>
 <tr>
  <th>Media Type</th>
  <th>Quality</th>
 </tr>
 <tr>
  <td>text/html;level=1</td>
  <td>1</td>
 </tr>
  <tr>
  <td>text/html</td>
  <td>0.7</td>
 </tr>
  <tr>
  <td>text/plain</td>
  <td>0.3</td>
 </tr>
  <tr>
  <td>image/jpeg</td>
  <td>0.5</td>
 </tr>
  <tr>
  <td>text/html;level=2</td>
  <td>0.4</td>
 </tr>
  <tr>
  <td>text/html;level=3</td>
  <td>0.7</td>
 </tr>
</table>

#### #전송방식
   - 단순 전송
     - <img width="600" alt="스크린샷 2023-04-18 오후 3 03 18" src="https://user-images.githubusercontent.com/79742210/233245523-b13bc214-c99c-42e4-9bb7-f2adc2ca7b04.png">
   - 압축 전송
     - <img width="600" alt="스크린샷 2023-04-18 오후 3 04 48" src="https://user-images.githubusercontent.com/79742210/233245607-b6f74c07-cd66-4f41-b733-ecf94e1664e5.png">
   - 분할 전송
     - <img width="600" alt="스크린샷 2023-04-18 오후 3 11 17" src="https://user-images.githubusercontent.com/79742210/233245686-ae1dc861-cf70-4ab2-8f58-e1e7449eb64c.png">
   - 범위 전송
     - <img width="600" alt="스크린샷 2023-04-18 오후 3 11 35" src="https://user-images.githubusercontent.com/79742210/233245769-adccdec0-c9da-4801-82c3-664745641e89.png">

#### #일반정보
 - From - 검색엔진
 - Referer
   - 현재 요청된 페이지 이전 웹 페이지 주소
   - 유입 경로 분석 가능
 - User-Agent
   - 클라이언트의 애플리케이션 정보
   - 어떤 정류의 브라우저에서 장애가 발생하는지 파악 가능
   - 요청에서 사용
 - Server
   - 요청을 처리하는 origin(proxy를 지나 진짜 요청하는 마지막 서버) 서버의 소프트웨어 정보
   - 응답에서 사용
 - Date
   - 메시지가 발생한 날자와 시간
   - 응답에서 사용

#### #특별한 정보
 - Host : 요청한 호스트 정보(도메인)
   - 요청에서 사용
   - 하나의 IP주소에서 여러 도메인이 적용되어 있을 때
   - <img width="600" alt="스크린샷 2023-04-18 오후 4 05 16" src="https://user-images.githubusercontent.com/79742210/233247735-de3edd60-bddb-4a3c-9a82-8555811193c2.png">
 - Location : 페이지 리다이렉션
   - 3xx 응답 결과에 Location 헤더가 있으면, Location 위치로 이동(리다이렉션)
   - 201 - Location 값은 요청에 의해 생성된 리소스 URI
   - 3xx - Location 값은 요청을 자동으로 리다이렉션 하기 위한 대상 리소스
 - Allow : 허용 가능한 HTTP 메서드
   - 405에서 응답에 포함해야함
 - Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

#### #인증
 - Authoriztion
   - 클라이언트 인증 정보를 서버에 전달
   - Authorization: Basic xxxxxx
 - WWW-Authenticate
   - 리소스 접근시 필요한 인증 방법 정의
   - 401 응답과 함께 사용

#### #쿠키
 - Set-Cookie : 서버에서 클라이언트로 쿠키 전달(응답)
 - Cookie : 클라이언트가 서버에서 받은 쿠키를 저장, HTTP 요청시 서버로 전달
 - <img width="600" alt="스크린샷 2023-04-18 오후 4 52 04" src="https://user-images.githubusercontent.com/79742210/233258170-f1aa5cbe-b726-4e5a-a82f-23baaaa6f613.png">
 - 특징
   - 사용처
     - 사용자 로그인 세션 관리
     - 광고 정보 트래킹
   - 쿠키는 항상 서버에 전송됨
     - 네트워크 트래픽 추가 유발
     - 최소한의 정보만 사용(세션 id, 인증 토큰)
     - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹스토리지(localStorage, sessionStorage) 사용
   - 보안에 민감한 데이터는 저장하면 안됨

 - 생명주기(Expires, max-age)
   ```shell
   Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
   ```
   - 만료일이 되면 쿠키  삭제
   ```shell
   Set-Cookie: max-age
   ```
   - 0이나 음수를 지정하면 쿠키 삭제
   - 세션 쿠키 : 만료 날짜를 생략하면 브라우저 종료시까지만 유지
   - 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지

 - 도메인
   - 명시
   ```shell
   domain=example.org -> 쿠키생성
   ```
    - 명시한 문서 기준 도메인 + 서브 도메인 포함
    - example.org & dev.example.org 쿠키 접근 가능
   - 생략
   ```shell
   example.org에서 쿠키 생성, domain 지정 생략
   ```
    - 현재 문서 기준 도메인에만 적용
    - example.org에서만 쿠키 접근, dev.example.org 쿠키 미접근

 - 경로
   ```shell
   path=/home
   ```
    - 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
    - 일반적으로 `path=/루트` 로 지정

 - 보안
   - Secure
     - 쿠키는 http, https를 구분하지 않고 전송
     - Secure를 적용하면 https인 경우에만 전송
   - HttpOnly
     - XSS 공격 방지
     - 자바스크립트에서 접근 불가(document.cookie)
     - HTTP 전송에만 사용
   - SameSite
     - XSRF 공격 방지
     - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송

---
### Header Cache

#### #캐시 기본 동작
 - 없을 때?
   - 데이터가 변경되지 않아도 계속 데이터를 다운로드 받아야함
   - 브라우저 로드 속도가 느려짐
 - 있을 때
   - 캐시 가능 시간동안 네트워크를 사용하지 않아도 됨
   - 브라우저 로드 속도가 매우 빠름
   - <img width="600" alt="스크린샷 2023-04-19 오전 10 53 45" src="https://user-images.githubusercontent.com/79742210/233260345-82fb1f9a-9a41-4890-9dea-4a7fca301f02.png">
 - 캐시 시간 초과
   - 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신(다시 저장)

#### #검증 헤더와 조건부 요청 0
 - 검증헤더
   - 검증헤더
     - 캐시 데이터와 서버 데이터가 같은 검증하는 데이터
     - Last-Modified, ETag
   - 조건부 요청 헤더
     - 조건에 따른 분기
     - If-Modified-Since : Last-Modified 사용
     - If-None-Match : ETag
     - 조건이 만족하지 않으면 304 Not Modified

#### #검증 헤더와 조건부 요청 1(Last-Modified)
 - 캐시 시간 초과(다시 요청했을 때 2가지 상황)
   - 서버에서 기존 데이터를 변경함
   - 서버에서 기존 데이터를 변경하지 않음
   - <img width="600" alt="스크린샷 2023-04-19 오전 11 29 16" src="https://user-images.githubusercontent.com/79742210/233261019-43c2272e-4a5f-4020-b063-3882bbc1a02d.png">
 - 서버의 데이터가 갱신되지 않으면 304 Modified + 헤더 메타 정보만 응답(Body x)
 - 클라이언트는 응답 헤더 정보로 캐시의 메타정보 갱신 + 캐시 저장 데이터 재활용<br>
   -> 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드
 - Last-Modified, If-Modified-Since 단점
   - 1초 미만(0.x초) 단위로 캐시 조정이 불가능
   - 날짜 기반의 로직 사용
   - 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우
   - 서버에서 별도의 캐시 로직을 관리하고 싶은 경우

#### #검증 헤더와 조건부 요청 2(ETag)
 - ETag(Entitiy Tag), If-None-Match
   - 캐시용 데이터에 임의의 이름을 달아둠
   - <img width="600" alt="스크린샷 2023-04-19 오후 1 58 55" src="https://user-images.githubusercontent.com/79742210/233261518-f04a0b37-7bb4-4bce-9695-a2ed68f92e22.png">
   - ETag만 서버에 보내서 같으면 유지, 다르면 다시 받기
   - 캐시 제어 로직을 서버에서 완전히 관리
   - 클라이언트는 단순히 이 값을 서버에 제공

#### #캐시 제어 헤더
 - Cache-Control : 캐시 제어
   - Cache-Control : max-age - 캐시 유효시간, 초 단위
   - Cache-Control : no-cache - 데이터는 캐시 가능하나, origin 서버에 검증하고 사용
   - Cache-Control : no-store - 데이터에 민감한 정보가 있으므로 저장하면 안됨
 - Pragma : 캐시제어(HTTP 1.0 하위 호환)
 - Expires : 캐시 유효 기간(하위 호환)
   - 캐시 만료일을 정확한 날짜로 계산
   - Cache-Control : max-age와 함께 사용하면 Expires는 무시됨

#### #프록시 캐시
 - <img width="600" alt="스크린샷 2023-04-19 오후 2 34 07" src="https://user-images.githubusercontent.com/79742210/233262274-47c12153-8dde-4b87-9b6a-12703e30cba6.png">
 - 캐시 지시어(directives)
   - Cache-Control : public
     - 응답이 public 캐시에 저장되어도 됨
   - Cache-Control : private
     - 응답이 해당 사용자만을 위함, private 캐시에 저장해야함(기본값)
   - Cache-Control : s-maxage
     - 프록시 캐시에만 적영되는 max-age
   - Age : 60(HTTP 헤더)
     - 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)

#### #캐시 무효화
 - 확실한 캐시 무효화 응답(혹시 모를 자동화 캐싱을 막기 위해서!)
   ```shell
   Cache-Contorl: no-cache, no-store, must-revalidate
   Pragma: no-cache
   ```
   - Cache-Control : no-cache
     - <img width="600" alt="스크린샷 2023-04-19 오후 3 11 14" src="https://user-images.githubusercontent.com/79742210/233262900-d5593650-96e8-4770-b144-97d1009fa2f2.png">
   - Cahe-Control : must-revalidate
     - <img width="600" alt="스크린샷 2023-04-19 오후 3 12 06" src="https://user-images.githubusercontent.com/79742210/233262993-8042f732-b483-4f75-80ba-cbf673b25b77.png">
