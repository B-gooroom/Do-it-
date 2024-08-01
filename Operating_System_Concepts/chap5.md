
## Chap 5. 스케줄링

### 기본개념
- 멀티프로그래밍에서 최대치로 CPU를 활용하는 방법
- 프로세스 실행 -> CPU와 I/O가 번갈아가면서 burst 타임이 생김
  - 파일 로딩중 - I/O가 루팡
  - I/O 대기상태 - CPU가 루팡
  - <img width="300" src="https://github.com/user-attachments/assets/a2ef7eaf-10dc-4d1b-a04e-3103ac6f812d" />

### CPU 스케줄러 (when?)
- 운영체제가 ready queue에 있는 프로세스 중 어떤 프로세스를 할당 할 것인가를 정하는 일
- 언제 실행하는가?
1.	running -> waiting state : I/O waiting (CPU 사용불가)
1.	running -> ready state : time sharing system
1.	waiting -> ready state : I/O 대기상태 -> ready
1.	terminate : 종료
  - 1 & 4 => non-preemptive (스스로 내놓음)
  - 2 & 3 => preemptive (쫓겨남)
---
### 스케줄링 기준 (Scheduling Criteria)
- (max)CPU 활용률 - CPU의 루팡 제어
- (max)처리량 - 일정한 시간 내에 최대한 많은 프로세스 실행
- (min)턴어라운드 - 프로세스 실행~종료까지의 시간 줄이기
- (min)대기시간 - ready queue에서의 대기시간 최소화
- (min)응답시간 - request 후 첫 번째 응답이 나올 때까지의 시간
---
### 스케줄링 알고리즘에는 아래 4가지 방식
1. FCFS
2. SJF
3. SRF
4. RR
---
### FCFS (First-come, First-Served)
- non-preemptive
- 선입선출 방식
- 비슷하게 들어오도라도 미세한 차이로 - 순서대로 진행
- 구현이 단순, 성능은 떨어짐
- Convoy Effect - 순서대로 들어오기 때문에 수행시간이 긴 프로세스가 먼저 들어오게되면, 뒤에 들어온 프로세스는 계속 기다리는 상황이 생김 -> Average waiting time이 늘어남
- <img width="600" src="https://github.com/user-attachments/assets/11ee18d3-c355-46f8-b386-594ef316bd80" />

### SJF(Shortest Job First)
- non-preemptive -> preemptive 형식으로 발전
- 프로세스 수행이 짧은 순서대로 프로세서에 할당
- FCFS에서 발생하는 convoy effect 해결 가능
- 버스트 시간이 큰 프로세스는 계속 뒤로 밀리는 현상(starvation)
- non-preemptive - avg = 4
- preemptive - avg = 3 (더 적음)
- <img width="600" src="https://github.com/user-attachments/assets/5527b99a-e758-4788-b7b2-00717187d984" />
- <img width="600" src="https://github.com/user-attachments/assets/49fc01c5-9b8e-4e55-9c47-a3ecdc42449f" />
- ! exponential averaging 계산법 ! (#15)

### RR (Round Robin, 돌리고돌리고)
- 일정 시간 할당량(Time quantum) 단위로 돌아가면서 CPU 할당
- preemptive가 선행되어야함
- 1 / n로 나눠서
- <img width="600" src="https://github.com/user-attachments/assets/f1f014be-76f2-4872-ba02-424755b93bfc" />
---
### 우선순위 스케줄링
- 각 프로세스에는 우선순위 번호(Priority Number)가 있음
- 작을 수록, 우선순위 높아짐 (priority 값의 우선순위 결정)
- SJF 방식
---
### 다단계 큐 스케줄링 (MultiLevel Queue)
- 각 대기열에는 고유한 스케줄링 알고리즘이 있음
- 우선순위 : 실시간 > 시스템 > 대화형 > 배치 순서
- interactive : foreground - RR
- batch : background - FCFS
### 다단계 피드백 큐 스케줄링 (MultiLevel Feedback Queue)
- 프로세스가 큐들 사이를 이동하는 것을 허용
- following parameters 존재
  - ex) 처음 들어오면 Q0(제로) -> Feedback으로 확인  후 추가 시간 부여 -> 이후 FCFS
- <img width="600" src="https://github.com/user-attachments/assets/1db4422b-9140-4bf4-8300-dcaff4d23dda" />

---
### Linux 스케줄링
- 두가지 알고리즘 - time-sharing, real-time
- (#더 찾아보기)
