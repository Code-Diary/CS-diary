# OS(운영체제) -operating system


##### [1.System Architecture(시스템 구조)](#System-Architecture)

##### [2.Process and Thread(프로세스와 쓰레드)](#Process-and-Thread)

##### [3.Scheduling(스케줄링)](#Scheduling)

---



## System Architecture

### 1. Operating-System Services
           
*운영체제가 사용자를 위해 제공하는 기능들은 다음과 같다.*

                  
- **사용자 인터페이스(User Interface)** :


  UI는 크게  CLI(Command-Line Interface), GUI(Graphical User Interface)로 나뉜다. 

  CLI는 과거 MS-DOS, 리눅스 터미널처럼 직접 명령어를 입력해 실행하는 방식이고,

  GUI는 윈도우나 Mac OS X 처럼 마우스를 통해 화면을 클릭하여 실행하는 방식이다.
  
        
- **프로그램 실행(Program execution)** 

  시스템은 프로그램을 메모리에 올려 실행시킬 수 있어야 한다. 이때 프로그램이 정상이던 비정상이던 실행을 끝낼 수 있어야 한다.

  

- **입출력 연산(I/O operation)**

  프로세스는 입/출력을 요구할 수 있다. 일반적인 사용자는 입/출력 장치를 제어할 수 없으므로 운영체제가 수행 수단을 제공해야 한다.

  

- **파일 시스템 조작(File system manipulation)** 

  파일을 읽고, 쓸 수 있으며, 이름으로 생성, 검색, 삭제가 가능해야 한다.  또한 접근 권한도 조정이 가능하다.

  

- **통신(Communication)** 

  여러 개의 프로세스가 메모리의 한 부분을 공유하도록 하는 <u>공유 메모리(Shared memory)</u>, 

  패킷(packet)을 사용해 시스템 간 프로세스 사이를 이동하는 <u>메세지 전달(Message passing)</u> 

  두 가지 방법을 사용한다.

  

- **오류 탐지(Error detection)** 

  운영체제는 가능한 모든 오류를 항상 의식하고 있어야 하고, 그에 따른 적당한 조치를 취할 준비가 되어 있어야 한다.

  

- **자원할당(Resource allocation)**

  운영체제는 다수의 사용자, 작업들이 동시에 실행될 때 각각에 대해 효율적으로 자원을 할당 할 수 있어야 한다.

  

- **회계Accounting)**

  운영체제는 특정 사용자, 작업이 어떤 시스템의 자원을 얼마나 사용하는지 확인할 수 있어야 한다.

  

- **보호(Protection)와 보안(Security)**

  보호는 기본적으로 시스템 자원에 대한 모든 접근이 통제되도록 보장하는 것을 말한다.  

  운영체제는 다양한 위협요소에 대한 보안정책을 수립할 필요가 있다.



### 2. System Calls (시스템 콜)

*운영체제는 커널 모드(Kernel Mode) 와 사용자 모드(User Mode)로 나뉘어 구동되는데, 이때 커널 영역의 기능을 사용자가 사용 가능하게 해주는 역할을 한다.*

시스템 콜은 아래와 같이 6가지로 분류할 수 있다.

- **프로세스 제어 :** end, abort, load, execute
- **파일 관리 :** create, delete, open, close, read, write
- **장치 관리 :** read, write, request, release
- **정보 유지 :** time, date
- **통신 :** send/receive messages, transfer status
- **보호** 



### 3. Operating System Structure

1.  ####  Simple Structure

   - MS-DOS 에서는 사실상 계층이 구분되어 있지 않아 Kernel에 직접 접근할 수 있었다. 즉, 사용자 프로그램에 문제가 생기면 전체 시스템에 문제가 생겼다.

     ex)

   - UNIX 에서는  MS-DOS와 비교하면 기능이 많이 분리 되었지만, 운영체제의 일반적인 기능을 커널과 동일한 메모리 공간에 적재, 실행하는 Monolithic kernel을 사용하여 유지보수가 쉽지 않았다.

     ex)

     

2.  #### Layered Approach (계층적 접근)

    운영체제의 복잡도를 낮추기 위한 방안이다. 이 방식은 유지보수가 편리한 장점이 있다.

    ex)

   

3. #### Microkernels (마이크로 커널)

   커널에서 핵심적인 요소만 남긴 가벼운 커널이고, 서버들 간 통신/에플리케이션의 서비스 콜 전달과 같은 기능을 한다.

   

4.  #### Modular kernel (모듈화 커널)

    커널을 확장하기 위한 기술로, 객체지향 프로그래밍 기법을 사용한다. 이 커널은 부팅 중 혹은 실행 중에 부가적인 서비스들을 링크한다. 

   

5. #### Hybrid Systems(혼성 구조)

   커널의 핵심만 남기고 나머지는 따로 구현한 시스템이다. Mac OS X, 안드로이드가 혼성 구조를 사용한다.
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





