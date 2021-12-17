# Job_Interview SW직무면접 대비용

1. 운영체제(Operating System)
	1. 프로세스 & 스레드(Process & Thread)
	2. 동기화(Synchronization)
	3. 인터럽트(Interrupt)
	
2. 자료구조 & 알고리즘
	1. 스택, 큐, 덱, 힙
	2. Sort
	3. 그래프
		1. 트리
		2. DFS/BFS
	4. 그리디
		1. 다익스트라
		2. 프림
	5. 다이나믹
	
3. 객체지향과 절차지향
	1. 객체지향
	2. 절차지향
4. C
	1. C의 특징
	2. 포인터
	3. 지역변수, 전역변수, 레지스터 변수, 정적변수
	5. C프로그램의 구조
5. Spring
	1. Framework
	2. Spring Framework
	3. Spring의 특징
	4. SpringMVC구조의 처리과정
	5. REST API
	6. Spring Annotation
6. 리눅스
	1. 리눅스 특징
	2. 리눅스 구조
	3. 리눅스 기본 명령어
7. JAVA

8. 
--------------------------------------------------------------------------------------------------------

#### 한번에 보기 편하게 하려고 위의 내용을 READ.md에 길게 썼습니다. 추후에 내용별 폴더를 정리해서 업로드 하겠습니다.

# 1. 운영체제(Operating System

**운영체제란?** :  컴퓨터 시스템의 자원들을 효율적으로 관리하며, 사용자가 컴퓨터를 편리하고, 효과적으로 사용할 수 있도록 환경을 제공하는 여러 프로그램의 모임입니다. 운영체제는 컴퓨터 사용자와 컴퓨터 하드웨어 간의 인터페이스로서 동작하는 시스템 소프트웨어의 일종으로, 다른 응용프로그램이 유용한 작업을 할 수 있도록 환경을 제공해 줍니다.

## i. Process(프로세스) & Thread(스레드)

프로그램 : 어떤 작업을 위해 실행할 수 있는 파일

**프로세스 : 실행중인 프로그램**

**스레드 : 프로세스의 실행 단위**

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

   new(생성)\
   Ready(준비)\
   Running(실행)\
   Waiting(대기)\
   Terminated(종료)

**스레드 구조**

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

이유 : 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 Context Switching 발생시 Stack 영역만 변경을 진행하면 되기 때문이다.


**멀티 프로세스(Multi Process)**

 : 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리하도록 하는 것.

 - 장점
 	- 여러 개의 자식 프로세스 중 하나에 문제가 발생하면 그 자식 프로세스만 죽는 것 이상으로 다른 영향이 확산되지 않는다. (안전성)
 - 단점
 	- Context Switching에서의 오버헤드 : 프로세스는 각 독립된 메모리 영역을 할당받았기 때문에 공유하는 메모리가 없다. 따라서 캐시 메모리 초기화 등의 무거운 작업이 진행되고 많은 시간이 소모되는 등의 오버헤드가 발생할 문제가 있다.
	- 프로세스 간 통신 기법 IPC : 프로세스는 각 독립된 메모리 영역을 할당받았기 때문에 프로세스들 사이에서 변수나 자료구조를 공유할 수 없다. 따라서 IPC라는 방법을 사용해야 하며, 이는 어렵고 복잡한 통신 방법이다.

**멀티 스레드(Multi Thread)**

 : 하나의 응용 프로그램을 여러 개의 스레드로 구성하고 각 스레드가 하나의 작업을 처리하도록 하는 것.

윈도우, 리눅스 등 많은 OS들이 멀티 프로세싱을 지원하고 있지만, 멀티 스레딩을 기본으로 하고 있다.

웹 서버는 대표적인 멀티 스레드 응용 프로그램이다.

 - 장점
	- 메모리 공간과 시스템 자원 소모가 줄어들게 된다.
	- 스레드 간 통신시, 전역 변수의 공간 또는 동적으로 할당된 공간인 Heap 영역을 이용해 데이터를 주고 받으므로 통신 방법이 간단하다.
	- Context switching 시, 캐시 메모리를 비울 필요가 없기 때문에 비용이 적고 더 빠르다.
	- 따라서 시스템의 처리량이 향상되고 자원 소모가 줄어들며, 자연스럽게 프로그램의 응답 시간이 단축된다.
 - 단점

	- 서로 다른 스레드가 Data, Heap 영역 등을 공유하기 때문에 어떤 스레드가 다른 스레드에서 사용중인 변수나 자료구조에 접근하여 엉뚱한 값을 읽어오거나 수정할 수 있다. 즉, 자원 공유의 문제가 발생한다.(동기화)
	- 하나의 스레드에 문제가 생기면 전체 프로세스가 영향을 받는다.
	- 주의 깊은 설계가 필요하며, 디버깅이 까다롭다

 **멀티스레드 Vs 멀티프로세스**
 
- 멀티 스레드는 적은 메모리 공간을 차지하고 Context Switching이 빠르다는 장점이 있지만, 오류로 인해 하나의 스레드가 종료되면 전체 스레드가 종료될 수 있다는 점과 동기화 문제를 가지고 있다.

- 멀티 프로세싱은 하나의 프로세스가 죽더라도 다른 프로세스에는 영향을 끼치지 않고 정상적으로 수행된다는 장점이 있지만, 많은 메모리 공간과 CPU 시간을 차지한다는 단점이 존재한다.

이 두 가지는 동시에 여러 작업을 수행한다는 점에서 같지만 적용해야 하는 시스템에 따라 적합/부적합이 구분된다. 따라서 대상 시스템의 특징에 따라 적합한 동작 방식을 선택하고 적용해야 한다.


## ii. 동기화

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
	register1 = counter		//register1 = 5
	register2 = counter		//register2 = 5
	register 1 = register1 + 1	//register1 = 6
	register 2 = register2 - 1	//register2 = 4
	counter = register1		//counter = 6
	counter = register2		//counter = 4

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

**세마포어**

: 공유된 자원의 데이터를 여러 프로세스, 스레드가 접근하는 것을 막음.

특징 : 동시에 접근할 수 있는 허용 가능한 갯수를 가지고 있는 Counter가 있음

   ex) 공용화장실에 칸이 4개일때 4칸이 비어있으면 기다릴 필요가 없음. 칸이 모두 차있으면 대기

문제점 : 소유가 불가능 -> 세마포어를 소유하지 않은 스레드가 세마포어를 해제가능

**뮤텍스**

: 공유된 자원의 데이터를 여러 프로세스, 스레드가 접근하는 것을 막음.

세마포어랑 비슷한데 갯수가 1개 & key가 존재.

: 일종의 Locking메커니즘 공유된 자원에 대한 접근을 조율하기 위해서 locking과 unlocking을 사용. lock에 대한 소유권이 있으며, lock을 가지고 있을 경우에만 공유 자원에 접근이 가능하고 lock을 가진 사람만 반납이 가능하다.

**모니터**

: 뮤텍스와 환경변수를 가지고 있는 동기화 매커니즘(?)

=> 뮤텍스와 세마포어 모두 완벽하지 않음. 기법을 사용하더라도 데이터 무결성을 보장할 수 없고 데드락이 발생할 수도 있다.


## iii. 인터럽트

**인터럽트** : 프로그램을 실행하는 도중 예기치 않은 상황이 발생할 경우 현재 실행중인 작업을 즉시 중단하고 발생된 상황을 우선 처리하도록 하는 것

**종류**
- 외부 인터럽트 : 입,출력장치, 타이밍 장치, 전원 등 외부적 요인으로 발생
	- 전원이상


--------------------------------------------------------------------------------------------------------
# 2.자료구조 & 알고리즘 간단 정리

## 스택

![stack](https://user-images.githubusercontent.com/45057466/97438280-ee94ff00-1967-11eb-9755-9dbfab889975.png)

  한 쪽 끝에서만 자료를 넣고 뺄 수 있는 선형 구조(LIFO - Last In First Out)
  
  push : 자료를 밀어 넣는다.
  
  pop : 가장 최근에 넣은(가장 위에 있는) 자료를 꺼낸다.
    
    
## 큐

![queue](https://user-images.githubusercontent.com/45057466/97438299-f3f24980-1967-11eb-8ee6-a65bcff7a813.png)

  뒤에서 자료를 넣고 앞에서만 뺼 수 있는 선형 구조(FIFO - First In First Out)
  
  push : 자료를 밀어 넣는다.
  
  pop : 가장 오래된(가장 앞에 있는) 자료를 꺼낸다.

  자바에서 큐는 스택과 달리 별도의 인터페이스 형태로 제공
  
  링크드리스트를 이용해서 큐 메모리 구조를 구현이 가능하다
  
## Heap

  우선 순위 큐를 위해서 만들어진 자료구조
  
  우선순위 큐 : 데이터들이 우선순위를 가지고 있고 우선순위가 높은 데이터가 먼저 나간다.
  

## Sort

**1. 선택 정렬(Selection Sort)**
 - 장점 : 구현이 쉽다. 공간적 효율이 좋다. 버블정렬과 시간복잡도는 같지만, 실제로 측정하면 버블보다는 조금 더 빠른 정렬방식
 - 단점 : 시간복잡도가 O(n^2) → 오래걸림
 - 시간복잡도 : O(n^2)
```java
for (int i = 0; i < arr.length-1; i++) {        // 1.
        indexMin = i;
        for (int j = i + 1; j < arr.length; j++) {  // 2.
            if (arr[j] < arr[indexMin]) {           // 3.
                indexMin = j;
            }
        }
        // 4. swap(arr[indexMin], arr[i])
        temp = arr[indexMin];
        arr[indexMin] = arr[i];
        arr[i] = temp;
  }
```
**2. 버블 정렬(Bubble Sort)**
 - 장점 : 구현이 쉽다. 코드가 직관적이다.
 - 단점 : 비효율적이다. 최악이든 최선이든 O(n^2)의 시간복잡도를 가짐
 - 시간복잡도 : O(n^2)

```java
for(int i = 0; i < arr.length; i++) {       // 1.
		for(int j= 1 ; j < arr.length-i; j++) { // 2.
			if(arr[j-1] > arr[j]) {             // 3.
                // swap(arr[j-1], arr[j])
				temp = arr[j-1];
				arr[j-1] = arr[j];
				arr[j] = temp;
			}
		}
	}
```

**3. 퀵 정렬(Quick Sort)**
 - 장점 : 시간적 효율이 좋음 → 기준값을 기준으로 분할을 통해서 구현하는 정렬법. 분할 과정에서 logN 이라는 시간이 걸림. 전체적으로 보게 되면 NlogN 으로써 실행시간이 준수한 편이다.
 - 단점 : 기준값에 따라서 시간복잡도가 크게 달라진다. Pivot이 적당한 이상적인 값이면 시간복잡도가 NlogN이지만 최악의 경우 O(N^2)
 - 시간복잡도 : O(NlogN), 최악의 경우 O(n^2)

**4. 힙 정렬(Heap Sort)**
 - 장점 : 추가적인 메모리를 필요로 하지 않으면서 항상 O(NlogN) 이라는 시간복잡도를 가지는 굉장히 정렬법들 중에서 효율적인 정렬법이라고 볼 수 있다.
 - 단점 : 실제 시간을 측정해보면 퀵정렬보다 느림. 데이터의 상태에 따라서 다른 정렬법들에 비해서 조금 느린편이다. 안정성을 보장받지 못함.
 - 시간복잡도 : O(NlogN)

**5. 병합 정렬(Merge Sort)**
 - 장점 : 퀵소트와 비슷하게 배열을 반씩 분할하면서 정렬하는 방법으로 logN만큼의 시간이 걸림 -> 최종적으로 NlogN의 시간이 걸림. 퀵소트와 달리, Pivot을 설정하는 과정이 없이 무조건 절반으로 분할하기 때문에 Pivot에 따라서 성능이 안좋아지는 경우가 없음
 - 단점 : 추가적인 메모리 필요
 - 시간복잡도 : O(NlogN)

**6. 삽입 정렬(Insertion Sort)**
- 장점 : 최선의 경우 O(N)
- 단점 : 최악의 경우 O(N^2) -> 데이터의 상태 및 크기에 따라서 성능의 편차가 심함.
- 시간복잡도 : 최선 O(N), 최악 




## 그래프 정의
  
  '정점(node)'과 '간선(edge)'으로 이루어진 자료구조
  
  간선의 방향 유무에 따라서 단방향 그래프와 양방향 그래프(무방향 그래프)로 나뉜다.
  
  완전탐색 문제 풀때 많이 씀
  
  그래프 탐색 기법 : DFS, BFS, 다익스트라, 플로이드와샬
  
  그래프 탐색 유형 : 미로, 정점 이동
  
## 트리

  ![tree](https://user-images.githubusercontent.com/45057466/97464210-f5ca0600-1983-11eb-959b-6861c5d116aa.png)
  
  
  그래프의 한 종류, 계층 구조를 나타내기 좋음.
  
  1. 1개의 루트 노드를 가짐
  
  2. 0개 이상의 서로 다른 자식 노드를 가짐
  
  3. 두 개의 노드를 연결하는 간선은 하나만 존재
  
  
  **트리는 싸이클이 존재하지 않음!!!**
  
  
## DFS/BFS

 
  ### DFS(Depth First Search : 깊이 우선 탐색)
  
  현재 정점에서 연결된 정점을 하나 골라서 파고들수 있는 최대한 깊게 파고 들어가며 탐색
  
  Stack을 이용 or 재귀를 이용
  
  재귀를 이용하면 매우 간단하게 짤 수 있음.

  <재귀를 이용한 DFS 함수>
  ```cpp
  vector<vector<int> > graph;
  bool visited[N];//노드에 방문했는지 여부 확인
  void dfs(int here){
        visited[here] = true; //노드에 방문 표시
        for( int i = 0; i<graph[here].size(); i++){
              int there = graph[here][i]; // 현재 노드와 연결된 노드를 there로 가져온다
              int(!visited[there]) // 만약 연결된 노드에 방문한 적이 없다
                    dfs(there);//there노드 방문
        }
  }
                                        
  int main(){
    for(int i = 0; i<graph.size(); i++){//만약 모든 노드가 다 연결 되어있다면 바로 dfs(start)하면 되지만 아닐 모든 노드가 연결되어있지않으면 확인 필요
      if(!visited[i])
        dfs(i);
    }
  }
```
  ### BFS(Breadth First Search : 너비 우선 탐색)
  
  현재 정점과 연결된 정점들에 대해 우선적으로 넓게 탐색
  
  Queue를 이용
  
  
  <Queue를 이용한 BFS 함수>
```cpp
	
vector<vector<int> > graph;
//vector<int> order; 정점의 방문순서가 필요할때
bool visited[N];
  void bfs(int start){
	queue<int> q;
	visited[start] = true; // 방문 표시
	q.push(start);//시작 노드를 큐에 푸쉬
	while(!q.empty()){
		int here = q.front();//방문할 노드를 here로 받아옴
		q.pop();
		//order.push_back(here);// 정점 방문 순서
		for(int i = 0; i<graph[here].size(); i++){
			int there = graph[here][i];// here노드와 연결된 노드들을 queue에 넣는다
			visited[there] = true;//노드를 
		}
	}
  }
                                        
  int main(){
    for(int i = 0; i<graph.size(); i++){
      if(!visited[i])
        bfs(i);
    }
  }
```
## 그리디 알고리즘

  욕심쟁이 알고리즘
  
  지금 가장 최적인 답을 선택해서 결과를 내는 알고리즘
  
  ***주의: 선택하는 순간에 최적이기 때문에 최종적으로 최적의 알고리즘이 아닐 수 있다.***
  
  그리디 사용 예시 : 다익스트라 알고리즘, 프림 알고리즘

## 다이나믹 프로그래밍

  하나의 문제는 단 한 번만 계산하도록 하는 알고리즘
  
  ### 다이나믹 프로그래밍의 조건
  
  1. 작은 문제가 반복이 일어나는 경우
  2. 같은 문제는 구할 때마다 정답이 같다.
  
  ### 구현방법

  1. Bottom-up : 작은 문제부터 차근차근 구해나가아가는 방법
  
  2. Top-down : 재귀 함수를 이용해서 구현, 큰 문제를 풀 때 작은 문제를 풀지 않았다면 그때 작은 문제 푸는 방법
  
  
  
  
# 3. 객체지향 Vs 절차지향

출처: https://demoversion.tistory.com/13 [Demoversion]

## 객체지향

1. 프로그램을 단순히 데이터와 처리 방법으로 나누는 것이 아니라, 프로그램을 수많은 '객체'라는 기본 단위로 나누고 이 객체들의 상호작용으로 서술하는 방식

2. 특징

	1. 캡슐화 : 객체의 속성(data fields)과 행위(methods)를 하나로 묶고 실제 구현 내용 일부를 외부에 감추어 은닉한다.
	2. 상속 : 새로운 클래스가 기존의클래스의 자료와 연산을 이용할 수 있게 하는 기능이다.
	3. 다형성 : 어떤 한 요소에 여러 개념을 넣어 놓은 것(오버라이딩, 오버로딩
	4. 추상화 : 공통의 속성이나 기능을 묶어 이름을 붙이는 것


3. 장단점 : 상속(편리하지만 구조가 이상하게 변할 수있음), 인스턴스에 데이터 접근 불가, 새로운 데이터 형식을 정의할 수 있게 해줌

## 절차지향

1. 루틴 서브루틴, 함수(프로시져) 등을 이용한 프로그래밍

2. 절차적으로 실행되는 것(X) -> 프로시져 콜, 즉 함수 호출을 통해서 재사용성을 얻어내는 것이 본질!

3. 장점 : 함수를 통한 코드의 재활용성 , 모듈화와 구조화에 용이함

4. 단점 : 프로시저 호출에 자원 낭비(최근 컴파일러, 하드웨어 성능향상으로 거의 상관없음)


-------------------------------------------------------------------------------------

# 4. C

1. C언어의 특징은?
    1. **C언어는 시스템 프로그래밍 언어이다.** 운영체제, 컴파일러, 편집기, 디버거 등 시스템 프로그램을 개발하는 도구
    2. **C언어는 함수 언어다.** 프로그램은 1개 이상의 함수 집합으로 구성된다. 작성된 함수는 분할해서 컴파일할 수 있으므로 쉽게 재사용할 수 있다.
    3. **C언어는 이식성이 강한 언어다.** 컴퓨터의 구조에 영향을 받지 않고 호환성을 유지한다. 이것이 가능한 이유는 모든 기계에서 동일하게 작동하는 다양한 표준 라이브러리가 제공되기 때문이다.
    4. 장점 : C로 짜여진 코드는 속도가 빠르고 바이너리 크기도 작아 속도가 다른 무엇보다 (심지어는 생산성보다도) 중요한 임베디드 혹은 모바일 계열, 또는 시스템 프로그래밍 등에서 주로 사용된다.

        ex) OS를 만든다면 아무리 생산성을 고려한다고 해도 시스템 제어 측면과 OS의 기능들 위에서 돌아가는 어플리케이션 때문에라도 속도라는 면은 중요하고, 그렇다고 속도를 높이기 위해 어셈블리어나 기계어로만 OS를 짜기에는 생산성이 매우 낮아지기 때문에, 타협점으로 C를 쓴다.

2. 포인터
    1. 일반 변수의 메모리 내 주소번지를 갖는 자료형이다. 변수명을 통하지 않고 사용하고자 하는 대상에 직접 접근할 수 있어서 프로그램이 간결하고 효율적으로 제어할 수 있다.
    2. 인자 전달 방법
        1. 인자를 값으로 전달(Call by value) : 함수가 호출되면 인자값을 스택으로 복사한다. → 함수에서 인자값을 바꿔도 메인에 영향을 끼치지 않음
        2. 인자를 주소로 전달(Call by reference) : 변수의 주소를 함수에 전달
    3. 포인터와 배열 관계 : 배열명은 그 자체로 해당 데이터가 있는 시작주소를 의미하는 포인터 상수

3. 지역변수, 전역변수, 레지스터 변수
    1. 지역변수 : 실행되는 단위 블록 내에서만 유효하고 선언된 블록의 영역을 넘어가면 효력없음.
    2. 전역변수 : 모든 블록에서 사용할 수 있으며 다른 파일에서도 사용할 수 있는 변수
    3. 정적변수 : 프로그램 실행이 끝날 때 까지 메모리에 계속 보존되는 변수
4. 절차지향언어란??? 객체지향언어란???
5. C프로그램의 구조
6. 시스템 라이브러리 함수와 사용자 정의 함수
7. 매크로

---------------------------------------------------------------------------------------------------------------------------------

# 5. Spring

1. Framework란?
    1. 특정 형태의 소프트웨어 문제를 해결하기 위해서 클래스 프레임과 인터페이스 프레임의 집합
    2. 특정한 틀을 만들어 놓고 거기에 살을 붙이면서 프로그램을 만들어서 작업시간을 줄여주는 것
    3. 프레임워크는 특정 개념들의 추상화를 제공하는 여러 클래스나 컴포넌트로 구성

    프레임워크를 사용하는 이유

    - 프로그램 개발에 투입되는 개발자가 늘어나면서 전체 시스템의 통합성, 일관성이 떨어짐 → 개발자의 자유를 제한

    프레임워크의 장/단점

    - 장점 : 개발 시간을 줄일 수 있고 오류로부터 자유로울 수 있다
    - 단점 : 처음에 익힐 시간이 필요하다?

2. Spring Framework(스프링 프레임워크)
    1. 자바(JAVA) 플랫폼을 위한 오픈소스 애플리케이션 프레임워크(Framework)이다.
    2. 자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크이다.
    3. 자바 개발을 위한 프레임워크로 종속 객체를 생성해주고, 조립해주는 도구
    4. 자바로 된 프레임워크로 자바 SE로 된 자바 객체(POJO)를 자바EE에 의존적이지 않게 연결해주는 역할
        1. 자바 SE : 데스크톱, 서버, 임베디드시스템을 위한 표준 자바 플랫폼
        2. 자바 EE : 자바를 이용한 서버측 개발을 위한 플랫폼
        3. POJO : 특정한 자바 모델이나 기능, 프레임워크르 따르지 않는 순수한 자바 객체
3. Spring의 특징
    - 경량 컨테이너로서 자바 객체를 직접 관리 : 각각의 객체 생성, 소멸과 같은 라이프 사이클을 관리하며 스프링으로부터 필요한 객체를 얻어올 수 있다.
    - 제어의 역행(IoC)
        - 객체의 생성, 사용, 소멸에 해당하는 생명주기의 관리를 애플리케이션 코드 대신 독립된 컨테이너가 담당한다.
        - 객체간의 연결관계를 런타임에 결정한다.
        - 객체간의 연결관계가 느슨해짐
    - DI : 의존성 주입
        - Spring IoC 컨테이너의 구체적인 구현 방식
        - 각 클래스 간의 의존관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것
        - 개발자들은 빈설정 파일에서 의존관계가 필요하다는 정보를 추가하면 된다.
        - 코드가 단순해진다
    - AOP(관점 지향 프로그래밍)
        - 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각각 모듈화 하는것
        - 간단한 설정만으로도 공통 기능을 여러 클래스에 적용할 수 있음
        - ex) 웹 애플리케이션의 보안, 로깅, 트랜잭션 등의 공통 관심 사항
    - 스프링은 영속성과 관련된 다양한 서비스를 지원 (ex. MyBatis, Hibernate등 이미 완성도가 높은 데이터 베이스 처리 라이브러리와 연결할 수 있는 인터페이스 제공)
    - 스프링은 확장성이 높음
4. Spring MVC구조의 처리과정

    ![Spring MVC 구조](https://user-images.githubusercontent.com/45057466/125324171-9c233380-e37a-11eb-8c1f-e6de1d3a95f2.png)


    - DispatcherServlet : 애플리케이션으로 들어오는 모든 Request를 받는 관문

        클라이언트의 요청을 전달받아 요청에 맞는 컨트롤러가 리턴한 결과값을 View에 전달하여 알맞은 응답을 생성

    - HandlerMapping : 클라이언트의 요청 URL을 어떤  컨트롤러가 처리할지 결정
    - Controller : 클라이언트의 요청을 처리한 뒤, 결과를 DispatcherServlet에게 리턴
    - ModelAndView : 컨트롤러가 처리한 결과 정보 및 뷰 선택에 필요한 정보를 담음
    - ViewResolver : 컨트롤러의 처리 결과를 생성할 뷰를 결정
    - View : 컨트롤러의 처리 결과 화면을 생성
    - 동작과정
        1. 클라이언트가 서버에 요청을 하면, front controller인 DispatcherServlet 클래스가 요청을 받는다.
        2. DispatcherServlet는 프로젝트 파일 내의 servlet-context.xml 파일의 @Controller 인자를 통해 등록한 요청 위임 컨트롤러를 찾아 매핑(mapping)된 컨트롤러가 존재하면 @RequestMapping을 통해 요청을 처리할 메소드로 이동한다.
        3. 컨트롤러는 해당 요청을 처리할 Service(서비스)를 받아 비즈니스로직을 서비스에게 위임한다.
        4. Service(서비스)는 요청에 필요한 작업을 수행하고, 요청에 대해 DB에 접근해야한다면 DAO에 요청하여 처리를 위임한다.
        5. DAO는 DB정보를 DTO를 통해 받아 서비스에게 전달한다.
        6. 서비스는 전달받은 데이터를 컨트롤러에게 전달한다.
        7. 컨트롤러는 Model(모델) 객체에게 요청에 맞는 View(뷰) 정보를 담아 DispatcherServlet에게 전송한다.
        8. DispatcherServlet는 ViewResolver에게 전달받은 View정보를 전달한다.
        9. ViewResolver는 응답할 View에 대한 JSP를 찾아 DispatcherServlet에게 전달한다.
        10. DispatcherServlet는 응답할 뷰의 Render를 지시하고 뷰는 로직을 처리한다.
        11. DispatcherServlet는 클라이언트에게 Rendering된 뷰를 응답하며 요청을 마친다.
    - DispatcherServlet의 장점 :  dispatcher-servlet이 해당 애플리케이션으로 들어오는 모든 요청을 핸들링해주면서 web.xml의 역할을 상당히 축소시켜주었다.
    - xml파일은 모두 객체(Bean)를 정의한다.
        - web.xml : Web Application의 설정(?)을 해주는 파일로서 XML 형식의 파일. ServletContext의 초기 파라미터, Session유효시간, Servlet/JSP에 대한 정의 및 매핑, Welcom File list 등이 작성됨
        - root-context.xml : 이 context에 등록되는 Bean들은 모든 context에서 사용되어 진다.(공유가 가능하다) 스프링 프로젝트 생성 시 root-context.xml에는 특별한 설정이 없다. 공통적으로 사용하려는 Bean을 그때그때 사용
        - servlet-context.xml : web.xml에서 DispatcherServlet 등록 시 설정한 파일. 이 context에 등록되는 Bean들은 servlet-container에만 사용되어진다.

5. REST API

- 웹(HTTP)의 장점을 최대한 활용할 수 있도록 만들어진 아키텍쳐
- REST API 구성
    - 자원(Resource) - URI
    - 행위(Verb) - HTTP METHOD
    - 표현(Representations)
        - URI란? 인터넷 자원을 나타내는 고유 식별자
- HTTP METHOD
    - 

    [제목 없음](https://www.notion.so/3c16b5b97f2846719ad17477fcd1affb)

- REST API 디자인 가이드
    - URI는 정보의 자원을 표현해야한다
    - 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.
- REST의 특징
    - 유니폼 인터페이스 : URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일
    - 무상태성 : 작업을 위한 상태정보를 따로 저장하고 관리하지 않는다. 세선 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API서버는 들어오는 요청만을 단순하게 처리하면 됨
    - 캐시 가능 : REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다. HTTP가 가진 캐싱 기능이 적용 가능하다.
    - 자체 표현 구조 : REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것입니다.
    - Client - Server 구조 : REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 됩니다.
    - 계층형 구조 : REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.

6.  Spring Annotation

- 컴파일러를 위한 정보를 제공하기 위한 용도.
- @를 이용해서 특별한 의미를 부여한다.
- 종류
    - Bean VS Component
        - 둘 다 목적이 명확하지 않을 때 사용
        - 각자 선언할 수 있는 타입이 정해져 있어 해당 용도 외에는 컴파일 에러가 발생
        - Bean : (개발자가 컨트롤 불가능한) 외부라이브러리들을 Bean으로 등록하고 싶을때
        - Componente : 개발자가 직접 컨트롤이 가능한 클래스일때
    - Controller VS WebServlet
        - 서블릿을 선언할 때 사용
        - Servlet Container에 의해 처리
        - WebServlet과 Spring MVC Controller는 같은 일을 하는 데 사용된다
        - Spring MVC의 Controller를 실행하기 위해서는 애플리케이션에 필요한 jar를 패키징해야 한다.
    - Service : 서비스영역
    - Repository : DAO


Android 할것!!

 - 4대 구성요소
 - Life Cycle
참고

[https://geminihoroscope.tistory.com/90](https://geminihoroscope.tistory.com/90)

[https://iri-kang.tistory.com/4](https://iri-kang.tistory.com/4)

[http://wiki.gurubee.net/pages/viewpage.action?pageId=26740333](http://wiki.gurubee.net/pages/viewpage.action?pageId=26740333)

[https://node-js.tistory.com/entry/Spring-webxml-root-contextxml-servlet-contextxml-역할Servlet-DispatcherServlet이란](https://node-js.tistory.com/entry/Spring-webxml-root-contextxml-servlet-contextxml-%EC%97%AD%ED%95%A0Servlet-DispatcherServlet%EC%9D%B4%EB%9E%80)

[https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)

[https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)

