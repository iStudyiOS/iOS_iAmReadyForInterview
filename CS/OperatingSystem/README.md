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
  
