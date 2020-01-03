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

#### 프로세스(Process)

​	연속적으로 실행중인 프로그램을 의미한다. 각 프로세스는 메모리에 적재 가능하며 CPU의 	할당을 받을 수 있다. 



​	**프로세스가 포함하는 것**

  1. Code 영역 : 프로그램 코드 등
  2. Stack 영역 : 지역변수, 매개변수, 리턴 값 등 임시 데이터로 사용.
  3. data 영역 : 전역변수, 정적변수, 배열, 구조체 등
  4. heap 영역 : 동적변수 등
  5. PC(program counter) , register

<img src="/assets/memory.png">

​	

​	**프로세스가 가지는 상태**

1. new : 프로세스 생성
2. running : 명령 실행
3. waiting : 특정 이벤트 발생했을 때 대기 상태에 들어감
4. ready : CPU를 할당 받기 위해 대기
5. terminate : 실행 종료

<img src="/assets/process state.png">



**PCB(Process Control Block)**

=> 특정한 프로세스를 관리할 필요가 있는 정보를 포함하는, 운영체제 커널의 자료구조

프로세스마다 하나씩 가지고 있음.

1. Process state : ready, running 등등
2. Process number : 프로세스 id
3. Program counter : 다음 실행할 명령어 주소
4. CPU registers
5. CPU scheduling information :  우선 순위, 최종 실행시각, CPU 점유시간 등 
6. Memory-management information  : 해당 프로세스의 주소 공간 등 
7. Accounting information  : 페이지 테이블, 스케줄링 큐 포인터, 소유자, 부모 등
8. I/O status information   : 프로세스에 할당된 입출력장치 목록, 열린 파일 목록 등



​	context switch가 발생할 때에 PCB를 저장하고 다른 프로세스의 PCB를 load하여 실행.



**프로세스 스케줄러**

1. job queue : 시스템의 모든 프로세스의 집합, secondary storage에 위치

2. ready queue : 실행 대기 상태에 있는 프로세스의 집합, 메모리에 위치

3. device queue : I/O device를 위한 프로세스 집합, 디바이스 컨트롤러에 위치

   

**장기스케줄러(Long-term scheduler or job scheduler)**

​	메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모	리(일반적으로 디스크)에 임시로 저장된다. 이 pool 에 저장되어 있는 프로세스 중 어떤 프로	세스에 메모리를 할당하여 ready queue 로 보낼지 결정하는 역할을 한다.

* 메모리와 디스크 사이의 스케줄링을 담당.

* 프로세스에 memory(및 각종 리소스)를 할당(admit)

* degree of Multiprogramming 제어  
  메모리에 여러 프로그램이 올라가는 것) 몇 개의 프로그램이 올라갈 것인지를 제어

* 프로세스의 상태  
  new -> ready(in memory)

  

_cf) 메모리에 프로그램이 너무 많이 올라가도, 너무 적게 올라가도 성능이 좋지 않은 것이다. 참고로 time sharing system 에서는 장기 스케줄러가 없다. 그냥 곧바로 메모리에 올라가 ready 상태가 된다._



**단기스케줄러(Short-term scheduler or CPU scheduler)**

* CPU 와 메모리 사이의 스케줄링을 담당.
* Ready Queue 에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정.
* 프로세스에 CPU 를 할당(scheduler dispatch)
* 프로세스의 상태  
  ready -> running -> waiting -> ready



 **중기스케줄러(Medium-term scheduler or Swapper)**

- 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄 (swapping)
- 프로세스에게서 memory 를 deallocate
- degree of Multiprogramming 제어
- 현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러.
- 프로세스의 상태
  ready -> suspended



**Context Switch(문맥 교환)**

​	CPU를 사용하고 있는 프로세스를 교환하기 위한 작업

​	바뀌기 전에 PCB에 저장을 한 후 바뀌게 된다. 이 작업은 overhead가 큰 작업이다.	



**Parent - child process**

=> 기본적으로 pid에 의해서 관리가 되며 부모자식간의 형태는 트리형태이다.

​	

​	자원공유

* Parent and children **share all resources**

* Children **share subset of parent’s resources**
* Parent and child **share no resources**



​	실행

* 부모와 자식은 동시에 실행

* 부모는 자식이 종료될 때까지 대기



​	fork를 이용하여 자식을 생성하며 자식은 부모와 같은 context를 가진다.

​	(program counter, register, memory info 등등)

​	

​	변수 pid 선언 fork();를 호출하면 커널모드가 된다. 프로세스는 fork가 리턴할 때 까지 기다린	다. 그리고 시스템콜은 커널에서 시행이 된다. 수행하고 나면 메모리에 새로운 PCB가 생기고 	부모의 PCB를 똑같이 복제하여 쓴다. 그리고 그 후에 둘 다 ready큐에 위치한다. 그리고 반환	이 된다. 이때 부모에게는 자식의 pid값을 자식에게는 0을 리턴 해준다. exec함수가 호출되는 	순간 이때 부모와 자식이 address space가 완전히 달라진다. Program count의 값이 초기화	된다. 자식이 새로운 address space를 가지게 된다. 부모는 자식이 돌아올 때까지 wait상태로 	대기한다.



​	**IPC(interprocess communication)**

​	=> 프로세스 사이에 communication을 하는 과정, 이를 통해서 프로세스간의 협업 가능



**message passing**

1.  Blocking(synchronous)
    - 발신 : 메세지를 보낸 후 응답이 올 때까지 대기
    - 수신 : available한 메세지를 받을 때까지 대기

2.  Non-Blocking(asynchronous)
    - 발신 : 메세지를 보내고 다른 작업 진행
    - 수신 : 정상적으로 수신하거나 안받음


​	**Buffering**

1. zero capacity : 발신자가 무조건 대기 (sync)
2. bounded capacity : n개의 메세지를 queue에 쌓아둠. 만약 queue가 꽉차면 발신자 대기
3. unbounded capacity : 무제한으로 메세지를 쌓아둠. 발신자는 대기 X



#### 쓰레드(Thread)

​	스레드(thread)란 프로세스(process) 내에서 실제로 작업을 수행하는 주체를 의미합니다. 모든 프로세스에는 한 개 이상의 스레드가 존재하여 작업을 수행합니다.

​	

​	**쓰레드 구성요소**

1. program counter

  2. register set

  3. stack space

     

​	**스택을 스레드마다 독립적으로 할당하는 이유**

​	스택은 함수 호출 시 전달되는 인자, 되돌아갈 주소값 및 함수 내에서 선언하는 변수 등을 저	장하기 위해 사용되는 메모리 공간이므로 스택 메모리 공간이 독립적이라는 것은 독립적인 	함수 호출이 가능하다는 것이고 이는 독립적인 실행 흐름이 추가되는 것이다. 따라서 스레드	의 정의에 따라 독립적인 실행 흐름을 추가하기 위한 최소 조건으로 독립된 스택을 할당한다.

​	**PC Register 를 스레드마다 독립적으로 할당하는 이유**

​	PC 값은 스레드가 명령어의 어디까지 수행하였는지를 나타나게 된다. 스레드는 CPU 를 할당	받았다가 스케줄러에 의해 다시 선점당한다. 그렇기 때문에 명령어가 연속적으로 수행되지 	못하고 어느 부분까지 수행했는지 기억할 필요가 있다. 따라서 PC 레지스터를 독립적으로 할	당한다.



​	**공유요소**

 1. code

 2. data

 3. files

  <img src="/assets/thread struct.png">



​	장점

1. 사용자에 대한 응답성 증가
   - 응용 프로그램의 일부분이 봉쇄 또는 긴 작업 수행 시에도 프로그램 실행을 계속 허용하여 사용자에 대한 응답성이 증가

2. 프로세스의 자원과 메모리 공유 가능
   - 스레드는 그들이 속한 프로세스의 자원과 메모리를 공유하므로, 응용 프로그램 하나가 같은 주소 공간에서 여러 개의 스레드를 실행, 시스템 성능 향상과 편리함 제공

3. 경제성
   - 한 프로세스의 자원을 공유하므로 프로세스를 생성하는 것보다 오버헤드를 줄일 수 있음

4. 다중 프로세서 구조 활용 가능
   - 다중 프로세서 구조에서 각 스레드는 다른 프로세서에서 병렬로  실행될 수 있음



​	**User thread**

​	=> OS는 thread의 존재를 모른다. OS는 프로세스에 모든 걸 할당하고 프로세스에서 thread 	library를 이용하여 일을 한다.(user level에서 이루어진다.) => 빨라진다

​	문제점 : 만약에 하나의 쓰레드라도 I/O를 만들어 내면 CPU는 프로세스가 I/O하는 줄 알고 전	체를 wait로 넣어버린다



​	**Kernel thread**

​	=> OS가 쓰레드를 지원해준다.

​	장점 : 쓰레드 하나가 I/O를 발생시켜도 그 쓰레드에 대해서만 wait가 들어간다. 할당 문제도 	OS가 해준다.

​	단점 : 만들 때도 커널이 만들어주고 죽일 때도 커널이 죽이기 때문에 느리다.



#### **쓰레드 이슈**

​	**fork시에 어떻게 자식 생성**

  1. fork이후에 exec를 바로 호출하면 모든 쓰레드를 복제할 필요가 없음.
     - 어짜피 새로운 프로그램에 의해서 새로운 쓰레드를 결정함.
  2. fork이후에 exec를 호출 안하면 모든 쓰레드를 복제해야함.



​	**Thread cancellation**

1. Asynchronous
   - 그냥 바로 쓰레드를 종료시킨다.
   - 데이터 문제 등 많은 문제가 발생할 가능성이 있으므로 주의해서 사용
2. Deferred
   -  순서에 맞게 체크를 통해 깔끔하게 종료를 시키는 것 



​	**Thread handling**

​	=> 시그널이 발생하면 프로세스에 전달 된다. Signal을 받는 놈(쓰레드)을 정할 필요가 있다. 	(os마다 정책적으로 결정한다)

 

​	**thread pool**

​	=> OS가 미리 쓰레드를 만들어두고 만들어 달라고 하면 바로 준다.

​	=> 필요시에 바로 줄 수 있지만 사용을 하지 않을 때는 불필요한 공간을 잡아먹는 것이다.

 

​	**Thread specific data(TSD)**

​	=> 전역변수라도 쓰레드들이 각각 다른 값은 assign하게 해준다.

​	=> 공유된 변수라 하더라도 쓰레드마다 처리하는 값은 다를 수 있다.


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





