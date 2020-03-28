# OS

**1.프로세스와 쓰레드의 차이**

프로세스란?
~~~
-   프로그램이 메모리에 올라간 상태 ( 프로그램의 인스턴스)
-   Code, Data, Stack, Heap의 구조로 된 독립적인 형태
-   기본적으로 메인스레드를 갖고 있다.
-   다른 프로세스의 변수나 자료구조에 접근할 수 없다. IPC를 통해 접근 가능(파이프, 파일 소켓 등)
~~~
쓰레드란?
~~~ 
-   프로세스 내에서 실행되는 흐름의 단위
-   프로세스가 할당받은 자원을 이용하는 실행의 단위
-   code, data, heap을 공유한다. 이를 통해 공유자원을 사용할 수 있다. ( 힙에 저장하면 받아쓰기)
-   바로 바로 반영이 되기에 이를 막아줘야 한다.
~~~
**2. 멀티 프로세스와 멀티 쓰레드의 차이**

멀티 프로세스
~~~
ex) fork를 통한 자식프로세스 생성 ( 모든 메모리 공간 복사 )

-   하나의 프로그램을 여러개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리하도록 한다. ( 하나의 자식 프로세스에 문제가 생겨도 다른 자식프로세스들에게 문제가 확산되지 않는다. )
-   IPC를 통한 자원공유를 해야한다.
-   Context Switching 오버헤드가 발생한다. (캐쉬, PCB) -> save state, reload state
~~~
멀티 쓰레딩
~~~
-   하나의 프로그램을 여러 개의 쓰레드로 구성하고 쓰레드로 하여금 작업을 처리하게 한다.
-   시스템 자원공유를 하기에 자원 할당 system call이 줄어든다.
-   단일 프로세스인 경우 효율이 좋지 않다.
-   멀티 프로세스인 경우 자원 공유 문제가 발생 (동기화 문제)
~~~
**3. 멀티 프로세스 대신 멀티 쓰레드를 사용하는 이유**
~~~
-   프로세스 간 Context Switching시 단순히 CPU 레지스터만을 교체하는 것이 아닌 RAM과 CPU사이의 캐쉬 메모리에 대한 데이터 까지 초기화 되기 때문
-   쓰레드는 code, heap, data를 공유하기 자원 소모가 줄어든다.
~~~
**4. PCB**
~~~
1.  프로세스 ID
2.  프로세스 상태 : READY / WAIT 등
3.  포인터 : 부모 프로세스에 대한 포인터, 자식에 대한 포인터, 프로세스가 위치한 메모리에 대한 포인터, 할당 된 자원에 대한 포인터
4.  CPU Registers : CPU 스케줄링에 필요한 레지스터 정보
5.  Priority : 스케줄링 프로세스 우선 순위
6.  할당된 자원 정보
7.  Account : CPU 사용시간, 실제 사용된 시간
8.  입출력 상태 정보
~~~
**5. Context Switching 수행 과정과 PCB 역할**
~~~
1.  CPU에서 현재 Running 상태였던 프로세스가 인터럽트가 걸린 경우 현재 내가 사용하는 레지스터에 대한 정보를 저장해야 한다. -> 다른 프로세스가 올라올 예정이니까.
2.  Cache 초기화. (공유하는 부분이 없으므로 캐쉬가 의미 없어진다.)
~~~
쓰레드인 경우 ?
~~~
1.  공유하는 부분이 있으므로 Cache에 있는 내용이 재사용 가능하다.
2.  Stack만 따로 사용하므로 PCB블록의 크기가 더 작다.
~~~
**6. Race Condition이란**
~~~
-   두 개 이상의 concurrent한 쓰레드들이 공유된 자원에 접근할 때 (동기화 하지 않고)
-   순서를 잘 조정해 주지 않으면 원하지 않는 결과가 생기게 된다.
~~~
**7. Inter-Process Communication**
~~~
-   Message Passing (Queue) (커널이 메시지 큐안에 넣고 이를 전달 -> 동기화 필요없음)

-   PIPE와 동일하지만 메모리공간(Message Queue)를 통해 전달

-   여러 프로세스가 이 데이터를 사용 가능

	1. indirect message passing : 커널이 전달해줌

	2. direct message passing : 어디에 넣어놓을 테니 가져가

-   Shared Memory : 동기화가 필요하다.

-   PIPE

	1. 익명 PIPE : 한 쪽은 읽기만, 한쪽은 쓰기만 -> half duplex / 같은 PPID 가질때 통신 가능

	2. Named PIPE : 모든 프로세스와 통신 가능 ( 단방향 )

-   Semaphore : 동기화 하고 보호하는데 목적을 둔다.
~~~
**8. Producer-Consumer Problem**
~~~
-   가정 : 4096바이트 버퍼가 있다. producer, consumer thread가 있다고 가정
-   Mutex 사용 : 서로가 critical section에 접근할 수 없다. (한쪽이 끝날 때 까지)
-   Semaphore 사용 : 4kb 버퍼를 1kb의 버퍼 4개로 나누고 ( 동시에 다른 버퍼에서 사용 )
~~~
  

**9. Mutex (acquire, release) / Semaphore (wait, signal)**
~~~
-   mutex가 binary semaphore과 같다고 생각하지만 약간 다르다.

-   mutex는 locking mechanism이다. (자원 접근에 대한 동기화 측면에서), mutex lock을 건 사람만이 release lock이 가능하다.

-   semaphore은 signaling mechanism이다. ISR(Interrupt Service Routine)을 통해 프로세스를 wake up 시켜주는 것
~~~
**10. Mutual Exclusion, Progress, Bounded Waiting**
~~~
-   ME : critical section에 다른 프로세스가 있을 경우 다른 프로세스는 접근이 제한된다.

-   Progress : 어떤 프로세스도 critical section에 있지 않는 경우 들어가려는 프로세스가 존재하면 누가 들어갈지 결정해야 한다.

-   Bounded Waiting : critical section을 요청한 프로세스는 무기한 대기해서는 안된다. 걸리는 시간에 한계가 있어야 한다.
~~~
  

**11. Busy waiting(Spin Lock) / Semaphore**
~~~
Mutex 단점

- busy waiting (while문에서 계속 반복됨 (spinlock) ) 싱글코어에서 치명적이다. 멀티코어에서 유용하다.


Semaphore 2가지 구현방법 : busy waiting / sleep queue

- sleep queue : 대기중인 프로세스를 관리한다. (context switching이 발생, 진입이 가능해진 경우(semaphore count가 양수가 되면) 깨운다.

- 현실에서는 hybrid를 사용, busy waiting조금 하다가 sleep queue로 들어간다.
~~~
**12. Peterson Algorithm**
~~~
-   공유 메모리를 사용할 경우 하나의 자원을 함께 사용하지 않도록 제어해주는 software적인 lock

-   flag, turn을 사용한 후 while문에서 들어가는 것을 차단
~~~
```c
flag[me] = true;
turn = other
while(flag[other] && turn == other) {
	wait();
}
criticalSection();
flag[me] = false;
```
**13. DeadLock**
~~~
1.  Mutual Exclusion : 공유자원에 접근이 제한된다.
2.  Hold and Wait : 공유자원을 갖고있는 프로세스가 양보하지않고 계속 갖고 있기 때문
3.  No preemption : 자원에 대해서 취소하거나 뺏을 수 없다.
4.  Circular Wait : 두 개 이상의 프로세스가 자원 접근을 기다리는데 cycle이 존재한다.
~~~
DeadLock 해결법(Prevention)
~~~
1.  Mutual Exclusion : 여러 개의 프로세스가 공유자원을 사용할 수 있도록 한다.
2.  Hold and Wait : 프로세스가 실행되기 전 모든 자원을 반환 / 프로세스가 시작 시 모든 자원을 할당받게 한다. (starvation)
3.  No preemption : 보유하고 있는 자원을 뺏을 수 있게 한다.
4.  Cirtular Wait : 자원에 순서를 부여한다. ( 철학자 식탁 )
~~~
Deadlock 해결법(avoidance)
~~~
-   banker’s algorithm / resource allocation graph (cycle)
-   max자원에서 이미 할당된 자원을 뺀 후 자원을 allocate했을 때 safe한지 확인 후 resource 할당
~~~
**14. Recovery from Deadlock**
Resource 관점
~~~
1. 자원 뺐기

2. safe state로 돌리기
~~~
Process 관점
~~~
1. 하나 프로세스 죽이기 (제일 일 안한 거 죽임)

2. 모든 프로세스 죽이기 (심각한 상황에서)
~~~