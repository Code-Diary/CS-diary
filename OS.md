# OS(운영체제) -operating system


##### [1.System Architecture(시스템 구조)](#System-Architecture)

##### [2.Process and Thread(프로세스와 쓰레드)](#Process-and-Thread)

##### [3.Scheduling(스케줄링)](#Scheduling)

---



## System Architecture

___







## Process and Thread

___








## Scheduling

*운영체제가 준비완료 큐(Ready queue)에 있는 프로세스들 중에서 어떤 프로세스를 디스패치(Dispatch)할 것인가 정하는 것을 스케줄링(Scheduling)이라고 한다.*  

*디스패치 : 프로세스를 CPU에 할당하는 것 ( 이때 프로세스 상태 ready -> running )*

### Scheduling Criteria

------

- CPU utilization(CPU 사용률) : CPU가 작업을 처리하는 시간의 비율
- Throughput(처리율) : 단위 시간 당 끝마친 프로세스의 수
- Turnaround time(반환시간) : 하나의 프로세스가 레디 큐에서 대기한 시간부터 작업을 마칠 때까지 걸리는 시간
- Wating time(대기시간) : 프로세스가 레디 큐에서 대기한 시간
- Response time(응답시간) : 프로세스가 처음 CPU를 할당받기까지 걸린 시간
___





