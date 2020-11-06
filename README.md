# Job_Interview
면접대비용

Algorithm
정렬
BFS&DFS
이분탐색

# Operation System
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





# 자료구조 & 알고리즘 간단 정리

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
 
**2. 버블 정렬(Bubble Sort)**
 - 장점 : 구현이 쉽다. 코드가 직관적이다.
 - 단점 : 비효율적이다. 최악이든 최선이든 O(n^2)의 시간복잡도를 가짐
 - 시간복잡도 : O(n^2)

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

  코딩테스트에서 난이도 높은 문제로 그래프 탐색이 많이 나옴! DFS함수와 BFS함수는 바로 짤 수 있을 만큼 익힐것!
 
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
  
