
## Chap 2. 시스템 구조 - System Structures

### 운영체제 서비스
- UI(User Interface) - 인터페이스 : CLI(shell에서), GUI(이이콘으로), Batch
- 프로그램 실행(Program execution) - 시스템은 프로그램을 메모리에 로드하고, 이를 실행 할 수 있어야함
- 입출력 명령(I/O operations) - 프로그램에는 I/O가 필요할 수 있음
- 통신(Communications) - 동일한 컴퓨터/ 네트워크를 통해 컴퓨터 간 정보 교환
- 에러 탐지(Error-detection) - 발생 가능한 오류를 지속적으로 인식해야함
### 운영체제 서비스 ver2. -> 시스템을 위한 작업
- 리소스 할당(Resource allocation) - 여러 사용자 또는 작업을 동시에 실행할 경우 컴퓨팅 자원은 각각 잘 분배되어야함
- 회계(Accounting) - 유저가 어떤 종류의 자원을 얼마나 사용하고 있는지 추척해야함
- 보호와 보안(Protection and Security) - 엑세스 허융범위 관리, 사용자 인증, 외부 I/O 장치의 잘못된 엑세스 시도로부터 보호하는 역할
---
### 시스템 콜(System Call)
- 커널과 사용자 프로그램을 이어주는 인터페이스 역할 (로우 레벨 작업 코드)
- 직접적인 호출 사용이 아닌 상위 API를 통해 프로그램에 엑세스
### 시스템 콜 실행(Implementation)
- 시스템 콜 테이블 : 메모리의 특정 주소 범위에는 호출에 대한 동작들이 할당 되어 있음
- OS 커널에서 의도된 시스템콜을 호출하고 시스템콜의 상태와 반환 값을 반환
- 호출자는 API를 준수하고 OS가 결과 호출로 수행할 작업을 이해하기만 하면 ok
- 런타임 지원 라이브러리에서 관리
- <img width="600" alt="chap1-1" src="https://github.com/user-attachments/assets/3d17a297-7ba2-451a-ab2f-ae995a5288ad">

### 파라미터 전달 (Parameter passing)
- 단순히 원하는 시스템 호출의 직별 정보보다 더 많은 정보가 필요한 경우
  - simplelest(call by Value) - register(cpu 메모리)에 저장, 대신 규모가 제한적 o
  - block/ table/ memory 방식(call by Reference) - 시작 주소를 register를 통해 전 (Linux, Solaris)
  - stack 방식 - 프로그램에 의해 스택/ 푸시, os에 의해 pop 되는 파라미터, 규모 제한 x
### 시스템 콜 타입
- 프로세서 제어(Process control) - end, load, execute
- 파일 관리(File management) - create, delete, open, close, read, write
- 디바이스 관리(Device management) - read, write, request, release
- 정보 유지 관리(Information maintenance) - get/set time, date
- 통신(Communications) - send/receive messages
---
### 계층
- simple structure
  - MS-DOS : 최소 공간에서 최고의 기능을 제공하도록 작성됨, 모듈 x, 사용자 프로그램이 입출력 루틴에 접근 - 디스플레이와 디스크 드라이브에 직접 접근 가능
  - UNIX : MS-DOS의 시스템 구조의 기능을 분리했지만, 하나의 계층이 너무 많은 일을 하는 것은 동일
- 계층적 접근(Layered Approach)
  - OS를 더 세분화해 계층을 분리한 방법
  - 가장 아래에 있는 계층(layer 0) = 하드웨어
  - 가장 높은 계층 (layer n) = 유저 인터페이스
  - 하나의 계층에만 신경쓰면 다른 계층은 신경 no~
- 마이크로 커널(Microkernels)
  - 최소한의 커널, 나머지는 ‘유저’의 공간을 씀
  - 장점 - 확장석이 높아짐, 포팅이 쉬워짐, 안전성 높아짐
  - 단점 - 유저 <-> 시스템간의 소통 overhead
- 모듈 (Modules)
  - 현재는 대부분 커널 모듈을 구현함
  - 객체 지향적 접근방식 사용
- 가상 머신(Virtual Machine)
  - 계층화된 접근 방식(layer approach)
  - 커널이 하드웨어인 것처럼 동작 - 실제 하드웨어는 1개인데 커널을 여러개로 돌려서 동작함
  - <img width="600" alt="chap1-1" src="https://github.com/user-attachments/assets/dcfaf9ee-aceb-4c8b-936e-ed04d7cafbed">
  - 가상 시스템 개념은 모두 각각 분리되어 있어서 시스템 리소스를 완벽하게 보호
  - 리소스를 직접 공유하는 것 x
  - 1개의 하드웨어를 다같이 공유, 마치 하드웨어에 직접 올라가 있는 것처럼 동작
  - <img width="600" alt="chap1-1" src="https://github.com/user-attachments/assets/54fdaee9-b6d4-46c0-b34d-91d59b87f913">
