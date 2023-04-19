## HTTP 웹 기본 지식

### 인터넷 네트워크

#### 인터넷 통신
<img width="600" alt="스크린샷 2023-03-24 오후 1 17 10" src="https://user-images.githubusercontent.com/79742210/232988601-6f2a1746-8c5e-4353-ad46-d24c256f1c55.png">

#### IP(Internet Protocol)
 - 지정한 IP 주소에 데이터 전달
 - 단위: `packet`(package + bucket)
 - <img width="600" alt="스크린샷 2023-03-24 오후 1 17 36" src="https://user-images.githubusercontent.com/79742210/232991547-f0c67c80-fde3-44e8-9a4a-18c8894b40ee.png">
 - `출발지 IP, 목적지 IP, data`
 - 한계
   - 비연결성 - 패킷의 대상이 없거나, 불능 상태여도 패킷이 전송됨(우편물 보내듯이)
   - 비신뢰성 - 패킷이 중간에 사라지거나, 요청 순서대로 오지 않는다면?
   - 프로그램 구분(중독성) - 같은 IP를 사용하는 서버에서 통신하는 app이 둘 이상일 때?

#### TCP
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

#### TCP
 - `IP + PORT + checksum` 정도만 
 - 하얀 도화지
 - http 3에서 udp 프로토콜을 적용함(단순하고 빠른 장점)

#### PORT
 - 같은 IP 안에서 프로세스 구분
 - <img width="600" alt="스크린샷 2023-03-31 오후 1 53 09" src="https://user-images.githubusercontent.com/79742210/233005142-0e18343e-fa81-4abf-94f0-06a52a6b03b7.png">
 - IP - 아파트 동, PORT - 아파트 호수
   - FTP - 20, 21
   - TELNET - 23
   - HTTP - 80
   - HTTPs - 443

#### DNS(Domain Name Service)
 - 도메인 명을 IP주소로 변환
 - IP 주소가 바뀌더라도, 접근이 가능함
 - <img width="600" alt="스크린샷 2023-03-31 오후 3 33 58" src="https://user-images.githubusercontent.com/79742210/233005543-ccc5e345-614d-41d9-8f49-bbe1d96bc737.png">

---
