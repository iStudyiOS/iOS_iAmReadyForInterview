# iOS


<details>
  <summary> AppDelegate, SceneDelegate가 각각 어떠한 라이프 사이클을 처리하는지 </summary>
  <br>
  
  - AppDelegate.  앱 실행 및 종료와 관련된 프로세스 라이프 사이클
  - SceneDelegate.  포그라운드와 백그라운드 상태에 있을 때 상태 전환과 관련된 UI 라이프 사이클

</details>

<details>
  <summary> 앱의 생명 주기 </summary>
  <br>
  
> 앱 실행 순서
> 

1. `application(_:didFinishLaunchingWithOptions:)`
    - 앱이 실행되면 앱을 화면에 보여주기 위한 모든 설정이 끝나고, 실제로 화면에 나타나기 직전에 호출

2. Scene 연결 (앱이 실행되면 UIKit에 Scene을 연결)
    - `application(_:configurationForConnecting:options:)`
        - 새로운 Scene을 만들고 UIKit과 연결하기 위한 configuration을 지정
        - 일반적으로 info.plist에 추가된 기본 값을 사용해서 생성
    
    - `scene(_:willConnectTo:options:)`
        - Scene이 연결된 것임을 delegate에 알려줌
        - `application(_:didFinishLaunchingWithOptions:)`에서 했던 UIWindow 생성 작업

- `sceneDidBecomeActive(_:)`
    - 앱이 inactive에서 Active 상태로 전환되었을 때 호출

3. To Background (OffScreen)
    - 앱 실행 후 홈 화면으로 나갈 때, Active - inactive - Background(Suspended)로 전환
    - SceneDelegate는 Scene에 다음 순서로 메서드 호출
        - `sceneWillResignActive(_:)`
            - Active → Inactive
        - `sceneDidEnterBackground(_:)`
            - Background 상태로 전환

4. To Foreground (OnScreen)
    - Background 상태에 있는 앱을 다시 실행하면 Background - Inactive - Active로 전환
    - SceneDelegate는 Scene에 다음 순서로 메서드 호출
        - `sceneWillEnterForeground(_:)`
            - Background → Inactive
        - `sceneDidBecomeActive(_:)`
            - Inactive → Active
  
</details>
  
<details>
  <summary> [동기(Sync)와 비동기(Async)], [직렬(Serial)과 동시(Concurrent)]의 차이점 </summary>
  <br>
  
    - 동기(Sync)와 비동기(Async)는?메인 쓰레드에서 대기열을 어떤 방식으로 처리할지?정하는 것.
    - 직렬(Serial)과 동시(Concurrent)는?어떤 대기열을 사용할 지?정하는 것
  
</details>
  
<details>
  <summary> 비동기 작업을 취소하는 방법 </summary>
  <br>
  
    - cancel 메서드를 통해 취소가 가능하다.
  
</details>
  
<details>
  <summary> Application States </summary>
  <br>
  
1. Not Running
  - 아예 실행되지 않았거나 앱이 종료된 상태

2. Inactive
  - 실행중이지만 이벤트를 받지 않는 상태. 예) 알림창 등을 가려진 상태, 잠금 상태
  
3. Active
  - 실행중이고 이벤트를 받는 상태
  - Active 상태로 들어오려면 Inactive 상태로부터 들어와야 한다
  
4. Background
  - Background에 있고, 코드를 실행중인 상태

5. Suspended
  - Background에 있지만, 코드를 수행하고 있지 않은 상태
  - 메모리에는 적재되어 있지만 메모리가 부족한 상황일 때는 앱을 죽이기도 한다.
  
</details>
  
<details>
  <summary> race condition을 피할 수 있는 방법 </summary>
  <br>
  
1. NSLock
  - Critical Section 전후로 NSLock의 lock, unlock 함수르 통해 쓰레드의 접근을 통제할 수 있다. 
  - 하지만, Deadlock을 유발할 수 있기 때문에 신중히 써야한다.
  
2. DispatcheSemaphore
  - Couting Semaphore의 구현체
  - 생성자로 넘겨주는 파라미터를 통해 초기 카운트 값을 정할 수 있다
  - wait와 signal 함수로 접근을 통제할 수 있다
  - wait를 통해 카운팅 1 감소, signal을 통해 카운팅 1 증가
  - wait를 호출했을 때 카운팅이 0이었다면, signal 함수가 불릴때까지 대기한다
  
3. Dispatch Barrier
  - Concurrent Queue에서 사용가능하다
  - .barrier flag를 설정한 코드 블럭은 큐에서 실행되는 유일한 작업임을 표시한다
  
4. Serial Queue
  - Serial Queue로 critical section을 wrapping을 해준다
  - Serial Queue를 통해 해당 코드가 하나의 쓰레드만 실행하도록 보장해준다
</details>


<details>
  <summary> 기존의 비동기 처리 방법과 async / await의 차이점은? </summary>
  기존의 비동기작업 시, 비동기처리, 분기처리 등의 클로저가 중첩된 형태로 작성하게 된다.

그렇게 되면...

- 가독성이 떨어지고
    
    ```swift
    // deeply-nested closures
    func processImageData1(completionBlock: (_ result: Image) -> Void) { 
    	loadWebResource("dataprofile.txt") { 
    		dataResource in loadWebResource("imagedata.dat") { 
    			imageResource in decodeImage(dataResource, imageResource) { 
    				imageTmp in dewarpAndCleanupImage(imageTmp) { 
    					imageResult in completionBlock(imageResult) 
    				} 
    			} 
    		}
    	 } 
    } 
    
    processImageData1 { image in 
    	display(image) 
    }
    ```
    
- 콜백은 오류처리를 어렵고 장황하게 만든다.
    
    ```swift
    // Using a `switch` statement for each callback: 
    func processImageData2c(completionBlock: (Result<Image, Error>) -> Void) { 
    	loadWebResource("dataprofile.txt") { 
    		dataResourceResult in 
    			switch dataResourceResult { 
    			case .success(let dataResource): 
    				loadWebResource("imagedata.dat") { imageResourceResult in 
    					switch imageResourceResult { 
    					case .success(let imageResource): 
    						decodeImage(dataResource, imageResource) { imageTmpResult in 
    							switch imageTmpResult { 
    							case .success(let imageTmp): 
    								dewarpAndCleanupImage(imageTmp) { imageResult in 
    									completionBlock(imageResult) 
    								} 
    							case .failure(let error): 
    								completionBlock(.failure(error)) 
    							}
    						} 
    					case .failure(let error): 
    						completionBlock(.failure(error)) 
    					} 
    			}
    		case .failure(let error): 
    			completionBlock(.failure(error)) 
    		} 	
    	} 
    }
    
    processImageData2c { result in 
    	switch result { 
    		case .success(let image): 
    			display(image) 
    		case .failure(let error): 
    			display("No image today", error)
    	}
    }
    ```
    

위의 문제를 해결하기 위해 `async-await proposal`은 swift의 `coroutine` 모델을 도입했다.

비동기 함수의 semetics를 정의하였으나 동시성을 제공하지는 않는다.
비동기 함수에서 `await`으로 흐름을 제어함으로써 동기적인 코드가 작성 가능하다.

```
- 비동기 코드가 마치 동기 코드인 것 처럼 작성할 수 있다.
- 클로저를 활용한 코드보다 상대적으로 가독성이 좋다.
```
</details>

<details>
  <summary> 'loadView()'와 'viewDidLoad()'의 차이는? </summary>
  
  > loadView()

  뷰 컨트롤러가 자신의 메인 뷰 (`self.view`)를 로드할 때 호출되는 메서드이다.

  즉, 그 메인 뷰를 생성하려고 호출하는 메서드 인것. 그래서 이 메서드 안에서 새로운 뷰를 만들어서 반환해줘도 된다. 
  ```
  스토리보드를 사용하는 경우, 스토리보드에 있는 뷰를 가져와 사용할 테니 굳이 사용할 필요가 없다.)
  ```

  > viewDidLoad()

  위의 뷰가 모두 생성되고 메모리에 올라간 후 호출되는 메서드 이다.

  즉 뷰컨트롤러의 메인 뷰가 생성된 이후 하고 싶은 작업에 대해서 작성하면 되는 메서드이다.

  ```
  간단하게 말하면,
  loadView()는 뷰가 로드되기 시작할 때 불려지고, viewDidLoad()는 뷰 로드가 완료된 후 불려진다.
  ```

  > 공식문서

  [loadView()란?](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621454-loadview)

  [viewDidLoad()란?](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621495-viewdidload)
</details>

<details>
  <summary> GCD의 종류와 사용 시 주의 사항은? </summary>

  > GCD의 종류

  - main: serial
      - DispatchQueue.main
      - 한개만 존재하고 `main thread`에서 동작한다.
      - 작업이 직렬로 처리되고
      - UI 처리를 담당한다.
  - global: concurrent / QoS 설정
      - QoS에 따라 6가지 종류가 있다.
      - 여러 스레드로 작업을 분산처리하여 동시처리 가능하다.
  - private: defualt로 serial(concurrent로 변경가능) / Qos 추론
      - QoS 설정이 가능하다.
      - 하지만 사실 굳이 설정해주지 않아도 OS가 알아서 QoS를 추론하게 된다.
      - label을 설정해주면 된다.

  - QoS란?
      - `Quality of Service` 의 약자
          - 중요도 순으로 처리를 하겠다는 뜻이다.
          - 종류로는 userInteractive, userInitiated, default, utility, background, unspecified 가 있다.
      
      ```swift
      // 유저와 직접 인터렉티브 : UI관련 (즉시)
      DispatchQueue.global(qos: .userInteractive)
      
      // 반드시 필요, 비동기 처리 : 앱 내에서 첨부파일을 열기, 내부 데이터베이스 조회 등 (몇초)
      DispatchQueue.global(qos: .userInitiated)	
      
      // 일반적인 작업
      DispatchQueue.global()	
      
      // ProgressIndicator와 함께 길게 사용되는 작업 : 지속적인 데이터 feed, Networking (몇초~몇분)
      DispatchQueue.global(qos: .utility)	
      
      // 사용자가 직접적으로 인지하지 않는 부분 : 데이터베이스 유지 등 (속도보다는 에너지 효율성 중시)
      DispatchQueue.global(qos: .background)
      
      // 사용하지 않음 legacy API
      DispatchQueue.global(qos: .unspecified)
      ```
      
      - 작업을 스레드에 배치하는 일은 OS가 알아서 처리한다.
      - 우선순위가 더 높은 큐의 작업을 우선적으로 더 많은 스레드에 배치한다.
      - 큐에도 우선순위를 매길 수 있지만, 작업을 대기열에 보내는 방식도 `QoS`를 매길 수 있다.

  > serial queue 상황

  - 한 번에 하나의 작업만 가능한데, async 작업이 2개가 존재하면 deadlock이 발생하게 된다.

  ```swift
  let testQueue = DispatchQueue(label: "testQueue") // concurrent선언하지 않았으므로 디폴트인 Serial Queue

  testQueue.async {
      testQueue.async {
          // 외부 블록이 완료되기 전에 내부 블록이 시작되지 않는 상태
          // 외부 블록은 내부 블록이 완료되기를 기다리는 상태
      }
      
      // 영원히 실행되지 않는 부분
  }
  ```

  → serial queue 를 concurrent queue로 변경한다.

  ```swift
  let testQueue = DispatchQueue(label: "testQueue", attributes: .concurrent)
  ```

  > DispatchQueue.main.sync의 deadlock

  - main은 메인 스레드에서 작업을 실행하는 전역적으로 사용 가능한 serial queue 이다.
      - concurrent queue가 아니고, run loop와 함께 동작한다.
      - run loop의 다른 이벤트 처리와 조율을 하는 역할을 한다.
  - main.sync를 호출하게 되면 앱의 이벤트를 처리하고 있던 main thread가 sync 호출에 의해 멈추게 되고 deadlock이 발생하게 된다.
      - backgroun thread와 main thread에서 이루어져야할 작업들을 순서에 맞게 사용해야 한다.
      - brackground threa 내에서 사용하는 것이 아니라면 Dispatchqueue.main.sync 사용을 지양하자!
</details>