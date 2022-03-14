# iOS


<details>
  <summary> AppDelegate, SceneDelegate�� ���� ��� ������ ����Ŭ�� ó���ϴ��� </summary>
  <br>
  
  - AppDelegate.  �� ���� �� ����� ���õ� ���μ��� ������ ����Ŭ
  - SceneDelegate.  ���׶���� ��׶��� ���¿� ���� �� ���� ��ȯ�� ���õ� UI ������ ����Ŭ

</details>

<details>
  <summary> ���� ���� �ֱ� </summary>
  <br>
  
> �� ���� ����
> 

1. `application(_:didFinishLaunchingWithOptions:)`
    - ���� ����Ǹ� ���� ȭ�鿡 �����ֱ� ���� ��� ������ ������, ������ ȭ�鿡 ��Ÿ���� ������ ȣ��

2. Scene ���� (���� ����Ǹ� UIKit�� Scene�� ����)
    - `application(_:configurationForConnecting:options:)`
        - ���ο� Scene�� ����� UIKit�� �����ϱ� ���� configuration�� ����
        - �Ϲ������� info.plist�� �߰��� �⺻ ���� ����ؼ� ����
    
    - `scene(_:willConnectTo:options:)`
        - Scene�� ����� ������ delegate�� �˷���
        - `application(_:didFinishLaunchingWithOptions:)`���� �ߴ� UIWindow ���� �۾�

- `sceneDidBecomeActive(_:)`
    - ���� inactive���� Active ���·� ��ȯ�Ǿ��� �� ȣ��

3. To Background (OffScreen)
    - �� ���� �� Ȩ ȭ������ ���� ��, Active - inactive - Background(Suspended)�� ��ȯ
    - SceneDelegate�� Scene�� ���� ������ �޼��� ȣ��
        - `sceneWillResignActive(_:)`
            - Active �� Inactive
        - `sceneDidEnterBackground(_:)`
            - Background ���·� ��ȯ

4. To Foreground (OnScreen)
    - Background ���¿� �ִ� ���� �ٽ� �����ϸ� Background - Inactive - Active�� ��ȯ
    - SceneDelegate�� Scene�� ���� ������ �޼��� ȣ��
        - `sceneWillEnterForeground(_:)`
            - Background �� Inactive
        - `sceneDidBecomeActive(_:)`
            - Inactive �� Active
  
</details>
  
<details>
  <summary> [����(Sync)�� �񵿱�(Async)], [����(Serial)�� ����(Concurrent)]�� ������ </summary>
  <br>
  
    - ����(Sync)�� �񵿱�(Async)��?���� �����忡�� ��⿭�� � ������� ó������?���ϴ� ��.
    - ����(Serial)�� ����(Concurrent)��?� ��⿭�� ����� ��?���ϴ� ��
  
</details>
  
<details>
  <summary> �񵿱� �۾��� ����ϴ� ��� </summary>
  <br>
  
    - cancel �޼��带 ���� ��Ұ� �����ϴ�.
  
</details>
  
<details>
  <summary> Application States </summary>
  <br>
  
1. Not Running
  - �ƿ� ������� �ʾҰų� ���� ����� ����

2. Inactive
  - ������������ �̺�Ʈ�� ���� �ʴ� ����. ��) �˸�â ���� ������ ����, ��� ����
  
3. Active
  - �������̰� �̺�Ʈ�� �޴� ����
  - Active ���·� �������� Inactive ���·κ��� ���;� �Ѵ�
  
4. Background
  - Background�� �ְ�, �ڵ带 �������� ����

5. Suspended
  - Background�� ������, �ڵ带 �����ϰ� ���� ���� ����
  - �޸𸮿��� ����Ǿ� ������ �޸𸮰� ������ ��Ȳ�� ���� ���� ���̱⵵ �Ѵ�.
  
</details>
  
<details>
  <summary> race condition�� ���� �� �ִ� ��� </summary>
  <br>
  
1. NSLock
  - Critical Section ���ķ� NSLock�� lock, unlock �Լ��� ���� �������� ������ ������ �� �ִ�. 
  - ������, Deadlock�� ������ �� �ֱ� ������ ������ ����Ѵ�.
  
2. DispatcheSemaphore
  - Couting Semaphore�� ����ü
  - �����ڷ� �Ѱ��ִ� �Ķ���͸� ���� �ʱ� ī��Ʈ ���� ���� �� �ִ�
  - wait�� signal �Լ��� ������ ������ �� �ִ�
  - wait�� ���� ī���� 1 ����, signal�� ���� ī���� 1 ����
  - wait�� ȣ������ �� ī������ 0�̾��ٸ�, signal �Լ��� �Ҹ������� ����Ѵ�
  
3. Dispatch Barrier
  - Concurrent Queue���� ��밡���ϴ�
  - .barrier flag�� ������ �ڵ� ���� ť���� ����Ǵ� ������ �۾����� ǥ���Ѵ�
  
4. Serial Queue
  - Serial Queue�� critical section�� wrapping�� ���ش�
  - Serial Queue�� ���� �ش� �ڵ尡 �ϳ��� �����常 �����ϵ��� �������ش�
</details>


<details>
  <summary> ������ �񵿱� ó�� ����� async / await�� ��������? </summary>
  ������ �񵿱��۾� ��, �񵿱�ó��, �б�ó�� ���� Ŭ������ ��ø�� ���·� �ۼ��ϰ� �ȴ�.

�׷��� �Ǹ�...

- �������� ��������
    
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
    
- �ݹ��� ����ó���� ��ư� ��Ȳ�ϰ� �����.
    
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
    

���� ������ �ذ��ϱ� ���� `async-await proposal`�� swift�� `coroutine` ���� �����ߴ�.

�񵿱� �Լ��� semetics�� �����Ͽ����� ���ü��� ���������� �ʴ´�.
�񵿱� �Լ����� `await`���� �帧�� ���������ν� �������� �ڵ尡 �ۼ� �����ϴ�.

```
- �񵿱� �ڵ尡 ��ġ ���� �ڵ��� �� ó�� �ۼ��� �� �ִ�.
- Ŭ������ Ȱ���� �ڵ庸�� ��������� �������� ����.
```
</details>

<details>
  <summary> 'loadView()'�� 'viewDidLoad()'�� ���̴�? </summary>
  
  > loadView()

  �� ��Ʈ�ѷ��� �ڽ��� ���� �� (`self.view`)�� �ε��� �� ȣ��Ǵ� �޼����̴�.

  ��, �� ���� �並 �����Ϸ��� ȣ���ϴ� �޼��� �ΰ�. �׷��� �� �޼��� �ȿ��� ���ο� �並 ���� ��ȯ���൵ �ȴ�. 
  ```
  ���丮���带 ����ϴ� ���, ���丮���忡 �ִ� �並 ������ ����� �״� ���� ����� �ʿ䰡 ����.)
  ```

  > viewDidLoad()

  ���� �䰡 ��� �����ǰ� �޸𸮿� �ö� �� ȣ��Ǵ� �޼��� �̴�.

  �� ����Ʈ�ѷ��� ���� �䰡 ������ ���� �ϰ� ���� �۾��� ���ؼ� �ۼ��ϸ� �Ǵ� �޼����̴�.

  ```
  �����ϰ� ���ϸ�,
  loadView()�� �䰡 �ε�Ǳ� ������ �� �ҷ�����, viewDidLoad()�� �� �ε尡 �Ϸ�� �� �ҷ�����.
  ```

  > ���Ĺ���

  [loadView()��?](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621454-loadview)

  [viewDidLoad()��?](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621495-viewdidload)
</details>

<details>
  <summary> GCD�� ������ ��� �� ���� ������? </summary>

  > GCD�� ����

  - main: serial
      - DispatchQueue.main
      - �Ѱ��� �����ϰ� `main thread`���� �����Ѵ�.
      - �۾��� ���ķ� ó���ǰ�
      - UI ó���� ����Ѵ�.
  - global: concurrent / QoS ����
      - QoS�� ���� 6���� ������ �ִ�.
      - ���� ������� �۾��� �л�ó���Ͽ� ����ó�� �����ϴ�.
  - private: defualt�� serial(concurrent�� ���氡��) / Qos �߷�
      - QoS ������ �����ϴ�.
      - ������ ��� ���� ���������� �ʾƵ� OS�� �˾Ƽ� QoS�� �߷��ϰ� �ȴ�.
      - label�� �������ָ� �ȴ�.

  - QoS��?
      - `Quality of Service` �� ����
          - �߿䵵 ������ ó���� �ϰڴٴ� ���̴�.
          - �����δ� userInteractive, userInitiated, default, utility, background, unspecified �� �ִ�.
      
      ```swift
      // ������ ���� ���ͷ�Ƽ�� : UI���� (���)
      DispatchQueue.global(qos: .userInteractive)
      
      // �ݵ�� �ʿ�, �񵿱� ó�� : �� ������ ÷�������� ����, ���� �����ͺ��̽� ��ȸ �� (����)
      DispatchQueue.global(qos: .userInitiated)	
      
      // �Ϲ����� �۾�
      DispatchQueue.global()	
      
      // ProgressIndicator�� �Բ� ��� ���Ǵ� �۾� : �������� ������ feed, Networking (����~���)
      DispatchQueue.global(qos: .utility)	
      
      // ����ڰ� ���������� �������� �ʴ� �κ� : �����ͺ��̽� ���� �� (�ӵ����ٴ� ������ ȿ���� �߽�)
      DispatchQueue.global(qos: .background)
      
      // ������� ���� legacy API
      DispatchQueue.global(qos: .unspecified)
      ```
      
      - �۾��� �����忡 ��ġ�ϴ� ���� OS�� �˾Ƽ� ó���Ѵ�.
      - �켱������ �� ���� ť�� �۾��� �켱������ �� ���� �����忡 ��ġ�Ѵ�.
      - ť���� �켱������ �ű� �� ������, �۾��� ��⿭�� ������ ��ĵ� `QoS`�� �ű� �� �ִ�.

  > serial queue ��Ȳ

  - �� ���� �ϳ��� �۾��� �����ѵ�, async �۾��� 2���� �����ϸ� deadlock�� �߻��ϰ� �ȴ�.

  ```swift
  let testQueue = DispatchQueue(label: "testQueue") // concurrent�������� �ʾ����Ƿ� ����Ʈ�� Serial Queue

  testQueue.async {
      testQueue.async {
          // �ܺ� ����� �Ϸ�Ǳ� ���� ���� ����� ���۵��� �ʴ� ����
          // �ܺ� ����� ���� ����� �Ϸ�Ǳ⸦ ��ٸ��� ����
      }
      
      // ������ ������� �ʴ� �κ�
  }
  ```

  �� serial queue �� concurrent queue�� �����Ѵ�.

  ```swift
  let testQueue = DispatchQueue(label: "testQueue", attributes: .concurrent)
  ```

  > DispatchQueue.main.sync�� deadlock

  - main�� ���� �����忡�� �۾��� �����ϴ� ���������� ��� ������ serial queue �̴�.
      - concurrent queue�� �ƴϰ�, run loop�� �Բ� �����Ѵ�.
      - run loop�� �ٸ� �̺�Ʈ ó���� ������ �ϴ� ������ �Ѵ�.
  - main.sync�� ȣ���ϰ� �Ǹ� ���� �̺�Ʈ�� ó���ϰ� �ִ� main thread�� sync ȣ�⿡ ���� ���߰� �ǰ� deadlock�� �߻��ϰ� �ȴ�.
      - backgroun thread�� main thread���� �̷�������� �۾����� ������ �°� ����ؾ� �Ѵ�.
      - brackground threa ������ ����ϴ� ���� �ƴ϶�� Dispatchqueue.main.sync ����� ��������!
</details>