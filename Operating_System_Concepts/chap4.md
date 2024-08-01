
## Chap 4. 스레드

### Threads 소개
- 스레드는 프로세스의 작업 흐름
- 하나의 프로세스가 한번에 하나의 작업만 수행하는 것 = Single Thread
- 하나의 프로세스가 동시에 여러 작업을 수행하는 것 = Multi Thread
- 스레드는 CPU 이용의 기본단위
### 스레드의 구성
- 스레드 ID
- 레지스터 세트
- 스택
- 프로그램 카운터(PC) (register set중의 하나)
- <img width="600" src="https://github.com/user-attachments/assets/fc868a79-aca7-419c-b920-882d8545aa44" />

### 멀티 스레드의 장점
- 응답성
  - 리소스 공유 (많은 자원들이 공유)
  - 경제적 (스레드 마다 필요한 부분들은 최소화)
  - MP 아키텍쳐의 활용방안
  - 각각의 플로우가 존재 (pc = program counter)
---
### User Treads & Kernel Treads
- User Treads
  - 사용자 수준의 스레드 라이브러리에서 스레드 관리 수행
  - 안정성은 떨어지지만, 성능 저하는 없음
  - POSIX P thread, Win32 thread, Java thread
- Kernel Treads
  - 커널이 지원하는 스레드
  - 안정적이지만, 유저 모드에서 커널모드로 계속 바꿔줘야하기 때문에 성능 저하
  - Window XP/2000, Solaris, Linux, Mac OS X
---
### 멀디스레딩 모델(Multithreading Models)
- Many-to-One
  - 유저 스레드 여러개 & 커널 하나
- One-to-One
  - 유저 스레드 하나 & 커널 하나
  - 요즘 대부분 one-to-one 방식을 사용 (window, Linux 등)
- Many-to-Many
  - 유저 스레드 여러개 & 커널 여러개
