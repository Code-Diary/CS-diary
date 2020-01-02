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



### Preemptive vs Non-preemptive ( 선점 vs 비선점 )



- Preemptive(선점) :  선점 스케줄링은 운영체제가 강제로 프로세스의  사용권을 통제하는 방식. 

  즉, CPU에 프로세스가 할당되어 있어도 운영체제가 개입해 강제로 다른 프로세스에게 CPU 할당이 가능하다.

- Non-preemptive(비선점) : 비선점 스케줄링은 프로세스가 스스로 다음 프로세스에게 자리를 넘겨주는 방식.

  즉, 프로세스가 종료되거나 IO request가 발생하여 자발적으로 대기 상태로 들어갈 때까지 계속 실행된다.

  

### Scheduling Criteria



- CPU utilization(CPU 사용률) : CPU가 작업을 처리하는 시간의 비율

- Throughput(처리율) : 단위 시간 당 끝마친 프로세스의 수

- Turnaround time(반환시간) : 하나의 프로세스가 레디 큐에서 대기한 시간부터 작업을 마칠 때까지 걸리는 시간

- Wating time(대기시간) : 프로세스가 레디 큐에서 대기한 시간

- Response time(응답시간) : 프로세스가 처음 CPU를 할당받기까지 걸린 시간



### Scheduling Algorithms



1. ####  FCFS(First-Come First-Served)

   - 먼저 CPU를 요청하는 프로세스를 먼저 할당하는 방식

   - Queue의 FIFO(First-In First-Out)와 동일하다.

   - 프로세스 처리 순서에 따라 성능이 크게 달라질 수 있다.

   - convoy effect(콘보이 효과)가 발생한다는 문제점이 있다.

     convoy effect : 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상

   - 비선점 스케줄링 방식
   

2.  ####  SJF (Shortest Job First)


    - 수행 시간이 짧은 프로세스를 우선 할당하는 방식

    - Waiting time(대기시간)을 줄이는 관점에선 SJF가 가장 좋다.
 
    - Starvation(기아)가 발생한다는 문제점이 있다. (Aging(에이징) 기법으로 해결 가능)

      Starvation : Burst time이 큰 프로세스는 계속 순서가 뒤로 밀려나 CPU를 할당받을 수 없는 현상

      Aging : 오래 있었던 프로세스일수록 우선순위를 높여주는 방식

    - 비선점 스케줄링 방식

   

3.  ####  SRTF (Shortest Remaining Time First)

    - 프로세스의 남은 수행 시간이 짧은 순서에 따라 할당하는 방식
    
    - SJF의 preemptive(선점) 버전
    
    - 각 프로세스의 burst time 추적, 선점을 위한 문맥 교환 등으로 인한 오버헤드가 크다는 문제점이 있다.  
    
    - 선점 스케줄링 방식

   

4.  ####  Priority Scheduling

    - 특정 기준으로 프로세스에게 우선순위를 부여해 그 순서에 따라 할당하는 방식

    - 프로세스를 Aging(에이징)해서 오래 대기한 프로세스의 우선순위를 높이는 방식으로 사용된다.

    - 다른 스케줄링 알고리즘과 결합해 사용할 수 있기 때문에 선점, 비선점 모두 가능하다.

      선점 스케줄링 방식 :  더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.

      비선점 스케줄링 방식 : 더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.

     

5.  ####  RR (Round Robin)

    - 프로세스들 사이에 우선순위를 두지 않고, Time Quantum(시간 단위)으로 여러 프로세스를 번갈아가며 할당하는 방식

    - Response time이 빨라진다.

    - 적당한 Time Quantum을 설정하는 것이 중요하다.

      Time Quantum -> ∞  : FCFS와 동일

      Time Quantum -> 0  : context switching overhead가 빈번하게 발생

    - 선점 스케줄링 방식

     

6.  ####  Multilevel Queue

    - 작업들을 여러 종류의 그룹으로 나누어 여러개의 Queue를 이용하는 방식

    - 각 Queue는 특성에 맞는 독립된 스케줄링 정책을 사용한다.

      ex)  foreground 작업은 RR 방식의 큐에, background 작업은 FCFS 방식의 큐에 둔다. 이렇게 하면 RR 방식의 큐에 많은 CPU 시간을 할당할 수 있다.

    - 각각의 Queue에 절대적 우선순위가 존재하며, Queue 간 이동이 불가능하다.

     

7.  ####  Multilevel Feedback Queue

    - Multilevel Queue에서 Queue 간 이동이 불가능한 점을 개선한 방식
    
    - 각 큐마다 다른 Time Quantum을 부여하며 시간안에 완료되지 못한 프로세스는 다음 단계 큐로 넘어간다.
    
    - 모든 프로세스는 가장 상위 큐로 들어오고, 다른 Queue로 점진적으로 이동한다.
    
    - 기아 상태 우려 시 Aging 기법을 사용해 우선순위 높은 Queue로 이동한다.
___





