## Chap 1. OS 소개 - Instruction

### 운영체제란? 종류와 목적
- 운영체제 (Operating System)는 컴퓨터의 하드웨어를 관리. </br>
  - 하드웨어와 소프트웨어, 사용자를 중개 역할을 하는 프로그램
- Kernel
  - 커널은 운영체제의 핵심.
  - 커널과 커널 모듈로 구성되고, 일반적으로 운영체제와 커널은 동일시 함
---
### 구성요소
- 컴퓨터 시스템은 4개의 구성요소로 나눌 수 있음
  - 하드웨어 : cpu, 메모리, 입출력 장치
  - 운영체제 (os) : 다양한 어플리케이션 <-> 사용자 간의 하드웨어 사용을 제어/ 조정
  - 다양한 어플리케이션 : 워드 프로세서, 컴파일러, 웹브라우저, DB시스템, 비디오게임
  - 사용자 : 사람, 기계, 기타 컴퓨터
  - <img width="600" alt="chap1-1" src="https://github.com/B-gooroom/Do-it-/assets/79742210/632a57ad-72b0-48ee-b8c6-277d926d310d.png">

- User View vs System View
  - UserView : 사용자가 컴퓨터를 쉽게 이용할 수 있도록 만들어줌
  - SystemView : 자원 할당자(Resource allocator), 제어 프로그램(Control program)
---
- 구성 (Organization)
  - 컴퓨터 시스템 = 여러개의 CPU & 장치 컨트롤러(device controller)
  - 이들은 공통버스(common bus)로 이어져 메모리를 공유함
  - <img width="528" alt="image" src="https://github.com/B-gooroom/Do-it-/assets/79742210/fcb46f42-3c89-482f-98c3-c32dd1411bd9">
---
- 운영방식 (Operation)
  - 입출력 장치 (I/O) 와 CPU를 동시에 실행할 수 있음
  - 장치 컨트롤러는 CPU에게 이벤트 발생 (이벤트 발생 알림 = Interrupt)
    - Interrupt - 하드웨어가 작동중에 CPU에게 알려주는 신호(signal)
    - Trap or Exception - 소프트웨어 오류 또는 요청으로 생성됨
  - 운영체제는 인터럽트 주도적, 인터럽트가 없다면 조용히 기다림
  - User Mode (Mode bit = 0) & Kernel mode (Mode bit = 1) -> dual mode
---
- 구조 (Structure)
  - 멀티 프로그래밍
    - 운영체제의 가장 중요한 부분 중 하나
    - CPU의 사용 효율을 높이는,,
    - 여러 프로그램을 메모리에 로드해 두고 어떤 프로세스가 대기 상태가 되면 다른 프로세스의 작업을 수행하는 시스템 (ex. I/O가 대기 상태일 경우 OS가 다른 작업으로 전환)
  - 타임쉐어링 (= 멀티태스킹)
    - 멀티프로그램을 확장 시킨 버전
    - 프로세스마다 작업시간을 정해두고 번갈아가면서 작업하는 방식
    - 프로세스들이 빠르게 번갈아가며 메모리를 사용하면 사용자 입장에서는 마치 동시에 작동하는 것처럼 보이게,,
    - response time은 1초 미만이어야함
    - 운영체제는 메모리에 자리가 없는 경우를 고려해 어떤 작업을 먼저 처리할 지 정해야 함 -> CPU Scheduling
    - 메모리를 너무 많이 사용하게 되는 경우 -> 가상 메모리 (Virtual memory)
