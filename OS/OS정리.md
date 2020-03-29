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

**15. 메모리관리 (partition Memory Management)**
~~~
1. Single contigous allocation : 계속 이어지는 하나의 메모리

2. Partitioned allocation : 메모리를 분할한 뒤 나눈다.

3. Paged memory management : 가상 메모리에서 사용되는 고정된 사이즈의 page frame으로 나눈다.

4. Segmented memory management : 다른 크기의 segment로 나눠 사용한다.
~~~
~~~
1.First Fit : 메모리 상단에서 맞는 공간에 할당

2. Best Fit : 가장 작으면서 잘 맞는 곳에 할당

3. Worst Fit : 가장 널널한 곳에 할당

4. Next Fit : First fit과 유사하지만 가장 마지막 할당부분에서 확인하면서 찾은 곳에 할당
~~~
Best Fit이 좋은것인가?
~~~
프로세서의 시간을 많이소요하며 fragmentation이 많이 발생한다.
~~~

**16. Virtual Memory in Operating System**
~~~
정의 : 보조 메모리를 메인 메모리의 일부인 것처럼 처리할 수 있는 스토리지 할당 체계다.

프로그램이 실행되기 위해서는 디스크에서 메모리로 갖고와야한다.

Main Memory와 register은 cpu가 바로 접근할 수 있는 저장공간이다.

base Address / limit Address는 logical address

base Address (relocation register)와 limit Address를 이용해 접근 x + base Addr

- Logical Address : CPU에 의해 생성되며 virtual address라 불림

- Physical Address : MMU에 의해서 보여지는 주소 (MMU가 virtual -> physical로 바꿔줌)

External Fragmentation : 모든 메모리 space에서 비는 공간

Internal Fragmentation : paging등에서 비는 부분
~~~
**17. Paging**
~~~
- 페이지란? -> virtual memory를 쪼개놓은 단위

- 프레임이란? -> physical memory를 쪼개놓은 단위
~~~
  
~~~
free memory는 항상 track된다. (free frame list)

p : page number (logical memory size가 2^m이고 page size가 2^n이면 (p = m – n))

d : page offset (page size가 2^n이면 n)

f : pagetable(p)

page table은 main memory에 있다. (PTBR (page-table base register)이 가리키고 있다.)

PTLR (page-table length register)는 페이지테이블에 길이를 나타낸다.

every data/instruction access는 2번의 메모리 access가 필요. ( p-table, data/instruction)

이를 방지하기위해 translation look-aside buffer(TLB)를 사용
~~~
**18. Demand Paging**
~~~
-   Demand Paging : 사용하는 부분만 메모리에 올리자
 
-   Valid, Invalid Bit를 사용한다.

-   메모리에 올리려는 것이 현재 메모리에 존재하는지 아니면 Disk에 존재하는지 알아야 한다.

-   bit = valid : 접근이 가능하며 실제 메모리에 올라와있다.

-   bit = invalid : 접근이 불가능하며 disk에 존재한다.
~~~
  
~~~
invalid bit인 경우 page fault(trap)이 된 후 디스크에 있는 data/instruction을 free frame인 physical memory에 올린 뒤 page table을 변경한 후 restart instruction

free frame이 없다면 page replacement를 해야하고 다음에도 이런 일이 생기지 않도록 잘 바꿔야한다.

1.  접근했을 때 invalid bit

2. victim frame을 설정,

3. victim frame에 정보를 disk에 저장 (swap out)

4. victim frame를 invalid로 변경

5. page를 가져와 victim frame자리로 올림

6. 현재 필요한 page에 대응하는 frame을 victim frame의 frame #으로 변경(swap in)

7. valid로 변경
~~~

Page replacement algorithm
~~~
1.  Optimal : 최적화된 replacement algorithm 하지만 미래 예측 불가, 측정 모델로 사용

2.  FIFO : 가장 먼저 들어온 frame이 나감

3.  LRU : 최근에 가장 안쓰인 frame이 나감
~~~
**19. Thrashing**
~~~
multiprogramming을 하면 CPU사용률이 적으면 새로운 프로세스를 시스템에 추가해서 다중프로그래밍의 정도를 높여준다. 그런데 페이지 테이블에서 현재 전에 사용하던 프로세스가 자주사용하던 페이지에 대한 paging fault가 발생하면 효율이 낮아진다.

방지하기 위해서 각 프로세스가 최소한 사용하는 프레임의 개수를 보장해줘야한다.
~~~
**20. Process Scheduling**
~~~
-   preemptive : Shortest Remaining time First(starvation), RR, priority(starvation / aging)

-   non-preemptive : FCFS, Shortest Job First (중간에 그만두지않고 쭉 이어감)

-   Multilevel Queue : 프로세스를 어떤 프로세스냐에 따라 그룹을 나누고 여러 개의 큐에 priority를 주어 이를 처리한다. ex) foreground process > background process prior
                       모두 ready queue로 나눈 뒤 이에 들어가서 이 순서대로 처리. 각 ready queue별로 처리

-   Multilevel Feedback Queue : quantum 8인 큐, 그다음 quantum 16, 그다음 FCFS
~~~

**21. Kernel Thread vs User Thread**
~~~
User Thread

- 스케줄링 우선순위가 없어 무슨 쓰레드가 먼저 수행될지 모른다.

-   커널은 쓰레드의 존재를 모른다.
-   동작중인 쓰레드가 blocking operation을 수행하면 모든 쓰레드가 멈춘다.
~~~
~~~
Kernel Thread

-   OS에 의해 구현되어있으며 OS가 존재에 대해 알고 있다.
-   사용자 쓰레드 한 개당 커널 쓰레드 한 개를 할당하면 overhead가 크다.
~~~