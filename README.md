# Job_Interview
면접대비용

Algorithm
정렬
BFS&DFS
이분탐색

Operation System
## Process(프로세스)

**프로세스 VS 프로그램**

프로그램 : 어떤 작업을 위해 실행할 수 있는 파일

프로세스 : 실행중인 프로그램

**PCB(Process Control Block)**

: 특정 프로세스에 대한 중요한 정보를 저장하고 있는 커널 내의 자료구조

👉커널 : 운영체제를 켤 때 맨처음에 실행되는 프로세스

- PCB에 저장되는 정보
    - 프로세스 식별자
    - 프로세스 상태
    - 프로그램 카운터
    - CPU 레지스터
    - CPU 스케줄링 정보
    - 메모리 관리 정보
    - 입출력 상태 정보
    - 어카운팅 정보

**프로세스 상태**

new(생성)
Ready(준비)
Running(실행)
Waiting(대기)
Terminated(종료)

**Thread(스레드)**

: 프로세스의 실행 단위

구조

code, data, stack, heap

**Context Switching(문맥 교환)이란?**
 : 여러 프로세스를 처리해야하는 상황에서 현재 진행중인 Task(프로세스, 스레드)의 상태를 PCB에 저장하고 다음에 진행할 Task의 상태값을 읽어서 적용하는 과정

과정

- Task의 대부분 정보는 Register에 저장되고 PCB로 관리된다.
- 현재 실행하고 있는 Task의 PCB 정보를 저장한다.
- 다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있다.

Context Switching은 많은 비용이 소모된다.

- Cache 초기화
- Memory mapping 초기화
- 커널은 항상 실행되어야 한다.
Context Switching의 비용은 프로세스가 스레드보다 더 많이 든다.
이유 : 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 Context Switching 발생시 Stack 영역만 변경을 진행하면 되기 때문이다

**프로세스 동기화(매우 중요 ⭐⭐⭐)**

공부할 것

- 경쟁 상태(race condition), 임계 구역(critical section) 문제에 대한 명확한 이해
- 임계 구역 해결 조건: 1. 상호 배제, 2. 진행, 3. 제한 대기
- 임계 구역 해결 방법
    - 피터슨 알고리즘 (데커, 램포트 빵집)
    - 하드웨어 솔루션: test_and_set, compare_and_swap
    - 뮤텍스, 세마포어 (in RTOS), 모니터 (in Java)

동기화(synchronization) : 한정적인 시스템 자원에 여러 스레드가 동시에 접근해서 사용하면 문제가 발생할 수 있기 때문에 이를 방지하기 위해서 여러 스레드에게 하나의 자원에 대한 처리 권한을 주거나 순서를 조정하는 기법.

race condition(경쟁 상태) : 두 개이상의 스레드가 공유된 자원에 접근하려고 할 때, 동기화 메커니즘이 없이 접근하려는 상황

ex) counter++를 실행할때, 어셈블리어는 3단계를 거쳐야함

register1 = counter
register1 = register1 + 1
counter = register

만약 counter++, counter--를 동시에 실행한다고 했을때, counter의 초기값이 5라면 결과값이 5가 되어야함.

but,

register1 = counter	register1 = 5
register2 = counter	register2 = 5
register 1 = register1 + 1	register1 = 6
register 2 = register2 - 1	register2 = 4
counter = register1	counter = 6
counter = register2	counter = 4

위와 같이 잘못된 결과가 나올 수 있음. 이를 해결하기 위해서 동기화가 필요로 함.

critical section(임계 영역) : 공유되는 자원에서 문제가 발생하지 않도록 독점을 보장해주는 영역

concurrent : multiprogram 하나의 CPU로 여러개의 프로그램을 돌린다.
parallel : multiprocess 여러개의 CPU로 하나의 프로그램을 돌린다.

**Critical Section(임계 영역) 해결 조건 3가지**

1.  Mutual exclusion(상호 배제) : 한 프로세스가 공유자원을 접근하는 critical section을 수행중일때는 다른 프로세스가 공유자원에 접근할 수 없다.
2. Progress(진행) :  critical section에 실행중인 process가 없을때 별도의 동작이 없는 프로세스 들만 critical section에 집입할 수 있다.
3. Bounded Waiting(한정된 대기) : 진입 신청 후 부터 진입까지의 waiting이 제한적이어야한다.

=> critical section문제를 해결하기 위한 프로그래밍 기법이 synchronization
=> race condition은 critical section현상을 설명하는 이론

세마포어
: 공유된 자원의 데이터를 여러 프로세스, 스레드가 접근하는 것을 막음.
특징 : 동시에 접근할 수 있는 허용 가능한 갯수를 가지고 있는 Counter가 있음
ex) 공용화장실에 칸이 4개일때 4칸이 비어있으면 기다릴 필요가 없음. 칸이 모두 차있으면 대기
문제점 : 소유가 불가능 -> 세마포어를 소유하지 않은 스레드가 세마포어를 해제가능

뮤텍스
: 공유된 자원의 데이터를 여러 프로세스, 스레드가 접근하는 것을 막음.
세마포어랑 비슷한데 갯수가 1개 & key가 존재.
: 일종의 Locking메커니즘 공유된 자원에 대한 접근을 조율하기 위해서 locking과 unlocking을 사용. lock에 대한 소유권이 있으며, lock을 가지고 있을 경우에만 공유 자원에 접근이 가능하고 lock을 가진 사람만 반납이 가능하다.

모니터
: 뮤텍스와 환경변수를 가지고 있는 동기화 매커니즘(?)

=> 뮤텍스와 세마포어 모두 완벽하지 않음. 기법을 사용하더라도 데이터 무결성을 보장할 수 없고 데드락이 발생할 수도 있다.

인터럽트

 - Mutual exclusion(상호 배제) : 한 프로세스가 공유자원을 접근하는 critical section을 수행중일때는 다른 프로세스가 공유자원에 접근할 수 없다.
 - Progress(진행) :  critical section에 실행중인 process가 없을때 별도의 동작이 없는 프로세스 들만 critical section에 집입할 수 있다.
 - Bounded Waiting(한정된 대기) : 진입 신청 후 부터 진입까지의 waiting이 제한적이여야한다.

 - Mutual exclusion(상호 배제) : 한 프로세스가 공유자원을 접근하는 critical section을 수행중일때는 다른 프로세스가 공유자원에 접근할 수 없다.
 - Progress(진행) :  critical section에 실행중인 process가 없을때 별도의 동작이 없는 프로세스 들만 critical section에 집입할 수 있다.
 - Bounded Waiting(한정된 대기) : 진입 신청 후 부터 진입까지의 waiting이 제한적이여야한다.
