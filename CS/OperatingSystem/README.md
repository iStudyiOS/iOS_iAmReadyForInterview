# OperatingSystem

<details>
<summary>동기와 비동기는 무엇인가요? </summary>
<div markdown="1">
    
- 동기는 현재 쓰레드에 작업중인 상황에 다른 작업이 들어오면 다른 쓰래드로 작업을 보내고 다른 쓰레드로 보낸 작업이 끝날때 까지 대기한 후, 작업이 끝나면 다른 작업을 시작한다. 
    
- 비동기는 반대로 다른 쓰레드로 작업을 보내도, 현재 쓰레드에 작업이 끝나면 다른 작업을 시작한다.
    
</div>
</details>
  
<details>
<summary>throttle()은 무엇인가요? </summary>
<div markdown="1">
    
- UI이벤트 처리에서 여러번 버튼을 눌러서 발생할 수 있는 에러를 방지하는 함수로, 이벤트를 일정 시간동안 한번만 실행되게 할수 있게한다.
    
</div>
</details>

<details>
<summary>Dispatch Group 은 무엇인가요? + 임계영역은 무엇인가요? </summary>
<div markdown="1">
    
- 멀티프로세스 환경에서 공유자원을 접근하는것에 있어서 생길수 있는 문제를 방지하기 위해 하나의 프로세스만 접근할 수 있도록 보장가능한 영역을 임계영역 이라고한다.
    
- iOS에서 임계영역 접근을 제한해야하는 문제를 해결하는 방법으로는 크게 두가지가 있는데, 하나는 DispatchGroup, 다른 하나는 DispatchSemaphore 이다.
    
- DispatchGroup 은 여러 프로세스를 각각의 큐에 넣은뒤 큐를 그룹화 시켜서 DispatchQueue에 추가하여 그룹에 추가된 모든 프로세스의 작업이 완료되면 그룹이 종료가 되는 방식이다.
    
- DispatchSemaphore은 Semaphore을 활용하여 다수의 작업이 하나의 공유자원에 접근할때 작업의 수를 제한하는 객체이다. wait()으로 카운팅값을 1만큼 감소하거나 0일 경우카운팅 값이 증가할 때 까지 대기하게 할 수 있고, signal()로 카운팅 값을 1만큼 증가하게 할 수 있게한다.
    
- DispatchGroup은 여러 작업이 모두 끝난것을 확인하고싶을때 유용하고, DispatchSemaphore은 최대 작업갯수를 제한하고 싶을때 유용하다.
    
</div>
</details>
  

<details>
<summary>Context Switching에 대해 설명해주세요</summary>
<div markdown="1">
<br>

- 하나의 프로세스가 CPU를 사용 중인 상태에서 다른 프로세스가 CPU를 사용하도록 하기 위해, 이전의 프로세스 상태를 보관하고 새로운 프로세스의 상태를 적재하는 작업
- 한 프로세스의 상태는 그 프로세스의 PCB에 기록됨

PCB란?
- 프로세스 제어 블록(Process Control Block)의 약자로, CPU에 의해 실행 중인 특정한 프로세스를 관리할 필요가 있는 정보를 포함하는 운영 체제 커널의 자료 구조

</div>
</details>


<details>
<summary>블록, 논블록에 대해 설명해주세요</summary>
<div markdown="1">
<br>

[참고자료](https://velog.io/@nittre/%EB%B8%94%EB%A1%9C%ED%82%B9-Vs.-%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EB%8F%99%EA%B8%B0-Vs.-%EB%B9%84%EB%8F%99%EA%B8%B0)

- 블로킹과 논블로킹은 ```제어권``` 이란 단어를, 동기(sync)와 비동기(async)는 ```리턴값```이란 단어를 기억하시면 됩니다.

### 블로킹
- A가 B를 호출하면, 제어권을 A가 호출한 B에 넘겨준다.
### 논블로킹
- A가 B를 호출해도 제어권은 그대로 자신이 가지고 있는다.
  
<br>

### 동기(sync)
- A가 B를 호출한 뒤, B의 리턴값을 계속 확인하면서 신경쓰는 것
### 비동기(async)
- A가 B를 호출할 때 콜백 함수를 함께 전달해서, B의 작업이 완료되면 함께 보낸 콜백 함수를 실행한다.
- A는 B를 호출한 후로 B의 작업 완료 여부에는 신경쓰지 않는다.


</div>
</details>


<details>
<summary>FCFS(First Come First Served)은 무엇인가요?</summary>
<div markdown="1">
<br>

- 먼저 온 고객을 먼저 서비스해주는 방식, 즉 먼저 온 순서대로 처리.
- 비선점형(Non-Preemptive) 스케줄링일단 CPU 를 잡으면 CPU burst 가 완료될 때까지 CPU 를 반환하지 않는다. 할당되었던 CPU 가 반환될 때만 스케줄링이 이루어진다.
- convoy effect(후위효과), 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다.

</div>
</details>