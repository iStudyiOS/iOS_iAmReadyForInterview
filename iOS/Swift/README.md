# Swift

<details>
<summary> mutating 키워드가 무엇인가요? </summary>
<div markdown="1">

- 스위프트에서 클래스는 레퍼런스 타입이고 구조체와 열거형은 값 타입이다. 값 타입은 기본적으로 인스턴스 메소드에서 내부 데이터를 수정할 수가 없다.

- 값 타입의 속성을 수정하려면 인스턴스 메서드에서 mutating 키워드를 사용해야 한다.

</div>
</details>


<details>
<summary> class, static, instance 메서드에 대해 설명해주세요 </summary>
<div markdown="1">

- 인스턴스 메소드 : 클래스, 구조체, 열거형의 인스턴스에 속한 메소드를 의미합니다. 클래스를 인스턴스화 후 해당 메소드를 호출해야한다.

- 타입 메소드 : class, static 키워드가 붙는다. 클래스를 인스턴스와 하지 않아도 바로 타입 자체에서 호출할 수 있다. class는 오버라이드 가능, static은 불가, final + class == static

</div>
</details>

<details>
<summary> 컬렉션타입, 구조체, 열거형, 클래스, 클로저를 값타입과 참조타입인지 나눠주세요 </summary>
<div markdown="1">

- 스위프트에서 모든 데이터타입(Int, Double, Set, Array, Dictionary 등등)은 모두 구조체 기반으로 구현되어있다. 구조체 기반이기 때문에 값타입이다. 열거형은 값타입이다.

- 클래스와 클로저(함수)는 참조타입이다.

</div>
</details>

<details>
  <summary> 컬렉션 타입의 종류와 특징에 대해 설명해주세요 </summary>
  <p>
      
  - 이름처럼 ‘데이터들의 집합'으로, swift에서는 ‘지정된 타입의 데이터들의 묶음’을 말한다.
    지정된(데이터) 타입이라고 하는 이유는 swift의 컬렉션 타입이 모두 Generic Collection으로 구현되어 있기 때문이다.

  - swift에서는 Array, Set, Dictionary 세 가지 컬렉션 타입이 있다.
    세 가지 타입은 변수로 생성하면 데이터 구성을 변경할 수 있고, 상수로 선언하면 변경할 수 없다.

  공식문서 노트에 따르면..

  > 컬렉션은 생성한 이후 수정할 필요가 없다면, 상수에 할당하는 것이 바람직하다. “앞으로 이 컬렉션은 수정하면 안 된다.”라는 의도를 코드에 명시하므로 다른 개발자가 코드를 이해하기 쉽다.
  또한 컴파일러의 성능 최적화(performance optimization)를 가능하게 한다.
  > 

  ### Array

  - 같은 데이터 타입의 값들을 순서대로 저장하는 리스트이다.
  - 중복 값을 저장할 수 있고, 순서가 있다. (순서가 있기에 중복값 구분 가능)

  ```swift
  var fruits: [String] = [] // 빈 배열로 초기화 및 선언
  fruits = ["apple", "banana", "kiwi", "apple"] // 값이 중복되어도 순서가 있으므로 상관없다.
  ```

  ### Set
  - 같은 데이터 타입의 값들을 순서없이 저장하는 리스트이다.
  - 순서가 없다는 점을 빼고는 Array와 비슷하다.
  - 순서가 없기 때문에 서로 같은 값을 구분할 수 없으므로 중복값이 허용되지 않는다.

  → 공식문서에서 ‘세트는 순서가 중요하지 않거나, 유일한 값일 때 사용하라.’고 적혀있다.

  - 집합 연산을 할 수 있다.
  - swift는 타입 추론을 하기 때문에, 만약 그냥 선언하면 배열로 인식해버린다.
  - 따라서 선언할 때 반드시 타입을 적어주어야 한다.
  - Set에 들어가는 값의 타입은 꼭 Hashable 프로토콜을 채택하고 있어야 한다.

  ```swift
  var lottos = Set<Int>()
  lottos = [1, 3, 1, 5, 8] // 배열과 같이 대괄호로 표현한다.

  // 중복값이 있는 상태로 대입해줄 수는 있지만, 프린트 해보면 중복값이 제거 되어있다.
  print(lottos) // 1,3,5,8
  ```

  ### Dictionary

  - 순서 없이 key 와 value가 한 쌍으로 데이터를 저장하는 컬렉션 타입이다.
  - key와 value에 대한 타입을 지정해놓으면 해당 타입만 입력할 수 있다. 
  (모든 key의 타입 동일, 모든 value의 타입 동일)
  - 마찬가지로 순서가 없다.
  - key의 타입은 꼭 Hashable 프로토콜을 채택하고 있어야 한다.
  - 정렬하고 싶다면, key 또는 value 프로퍼티에 대해서 sorted()를 사용할 수 있다.

  ```swift
  var phoneBook: [String: String] = [:] // String타입의 key, String타입의 value인 딕셔너리 초기화 및 선언
  phoneBook["홍길동"] = "010-1111-1111" // 딕셔너리에 값 넣기
  phoneBook["김철수"] = "010-2222-2222"

  print(phoneBook["홍길동"]) // 010-1111-1111
  ```
  </p>
</details>

<details>
  <summary> 옵셔널이란 무엇인지, 옵셔널값을 unwrap하는 방법에 대해 설명해주세요.</summary>
  <br>

  - 옵셔널은 변수의 값이 `nil` 일 수 있다는 것을 표현하는 것이다.
  - 반대로 Optional이 아니라면(non-optional) 해당 값은 nil이 될 수 없음을 의미한다.

  ```swift
  var name: String? // ? 키워드를 사용

  var age: Int // 컴파일 에러
  var age = nil // 컴파일 에러
  ```

  - Optional 키워드를 사용하지 않았다면 값을 입력하라는 에러가 발생하고, 이후에도 `nil`을 넣으려고 하면 컴파일 에러가 발생한다.
  - `nil`을 가질 가능성이 있는 값은 컴파일 단계에서 에러를 발생시키기 때문에 unwrapping, binding 과정이 필요하다.

    <details>
      <summary> 1) Optional Unwrapping </summary>
      <br>

      ```swift
      var number: Int? = 10

      if number {
      let double = number! + number! // forced unwrapping
      }
      ```

      - `!` 키워드를 통해 강제로 값을 꺼내온다.
      - 만약 if로 `nil` 체크를 하지 않고 `!`를 사용한다면 런타임 에러가 발생할 수 있으므로, `!` 사용은 최대한 피하는게 좋다.

    </details>

    <details>
      <summary> 2) Optional Binding </summary>
      <br>

      - 변수에 값이 있을지 없을지 모르는 상황에서 Optional을 우리는 사용해야 하지만 그 값을 안전하게 추출하기 위해서 사용하는 방법이 Optional Binding이다.
      - Optional Binding에는 `if let`, `guard let` 두 가지가 있다.
      <br>
      
      **[ if let ]**
      ```swift
      // if let
      var number: Int? = 10

      if let number = number {
      print("number is \(number)") // number에 값이 있는 경우
      } else { // number에 값이 없는 경우
      print("number does not exist.")
      }
      ```

      - `Optional`값을 새로운 상수로 받고, if문의 괄호 안에서는 `non-optional`값을 사용한다.
      - 새로 선언된 상수는 `non-optional` 값이기 때문에 `!` 키워드를 사용할 필요가 없다.
      <br>
      
      **[ guard let ]**
      ```swift
      // guard let
      var number: Int? = 10

      guard let number = number else { return }
      ```

      - `Bool` 타입의 값으로 `guard`문을 동작시킬 수 있지만, 옵셔널 바인딩 역할도 가능하다.
      - `guard` 문은 항상 `else` 구문이 따라오고, `else` 블록 내부 코드에 자신보다 상위 코드 블록을 종료하는 코드가 반드시 들어가게 된다.
      - 코드 블록 종료 시 `return, break, continue, throw` 등 **“제어문 전환 명령어”**를 사용한다.

    </details>

    <details>
      <summary> 3) guard VS if let 특징 비교 </summary>
      <br>

      **[ guard문의 특징 ]**
      - 반드시 ‘제어문 전환 명령어'를 넣어주어야 한다.
      - 요구사항 조건 코드를 if let 보다 훨씬 간결하고 읽기 좋게 구성이 가능하다.
      - 예외 사항만 처리하고 싶을 때 좋다. ← [예외처리의 예시](https://dev200ok.blogspot.com/2020/03/swift-guard-let-if-let_24.html)
      - 함수 전체에서 optional로 추출된 상수나 함수를 사용할 수 있다.
      <br>
      
      **[ guard문 사용시 주의 사항 ]**
      - 제어문 전환 명령어를 쓸 수 없는 상황이라면 사용이 불가능하다.
      - 함수, 메서드, 반복문 등 특정 블록 내부에 위치하지 않는다면 사용이 제한된다.
      <br>
      
      **[ if let의 특징 ]**
      - 성공과 실패 2가지로 나누어서 원하는 작업이 가능하다.
      - 지역 변수로만 사용이 가능하다.
      - else문을 생략할 수 있다.
      - 옵셔널 바인딩된 상수는 그 블록 안에서만 변수 사용이 가능하다.
      <br>
      
      **[[ 언제 사용하면 좋을까? ]](https://www.hackingwithswift.com/quick-start/understanding-swift/when-to-use-guard-let-rather-than-if-let)**
      - guard : 예외 사항만 처리하고자할 때 사용하면 좋다.
      - if let : 조건을 가지고 나누어 처리할 때 사용하면 좋다.

    </details>

    <details>
      <summary> 4) Coalescing Nil Values </summary>
      <br>

      ```swift
      var number: Int? = 10
      print(number ?? 0) // number가 nil일 경우 0을 대신 출력
      ```

      - `Optional Int`타입의 number에 값이 들어있다면 unwrapping하고, `nil`일 경우 default값으로 `??` 뒤에 적힌 값을 반환하는 operator 이다.
    </details>
</details>

<details>
<summary>class, struct는 공통점이 무엇인가요?(언제 사용하나요?)</summary>
<div markdown="1">

  1.  서로 다른 타입들을 하나로 묶을 수 있다.
  2.  묶은 자료형들을 새로운 타입처럼 사용 가능하다.
  3.  클래스, 구조체 안에 함수나 프로퍼티를 정의할 수 있다.
  4.  extension이 가능하다.

</div>
</details>

<details>
  <summary> 클래스와 구조체는 언제 사용하면 좋을까요? </summary>
  <br>
  
  ## [ 클래스 < 구조체 ]
  ```
  - 구조체는 값타입으로 불변성을 유지하기 때문에 여러 스레드들이 한 인스턴스를 사용하는 다중 스레드 환경에서도 안전하게 사용될 수 있다.
  - 구조체는 `Stack`에 저장하기 때문에 인스턴스 생성이 더 빠르다.
  - `Heap`에 저장되는 클래스는 `Heap`에 인스턴스를 저장하고, 그 참조값을 `Stack`에 저장한다.
  ```
  <br>
  
  ## [ 클래스 > 구조체 ]
  ```
  - 구조체는 값타입이기 때문에 값이 같은 인스턴스가 매번 복사되어 사용되는데, 
    만약 어떤 인스턴스의 참조값의 고유성을 유지하고 싶다면 클래스를 사용한다.
  ```
</details>

<details>
  <summary> 타입 캐스팅을 할 떄 사용하는 as, as?, as!의 차이첨은 무엇일까요? </summary>
  <br>
  
  ## 타입 캐스팅(Type Casting) 이란?
  > 인스턴스의 타입을 확인하거나 클래스 계층의 다른 부모 클래스/자식 클래스로 취급하는 방법이다.
  
  ## 다운 캐스팅
  > 부모 클래스 -> 자식 클래스로 형변환 / 자식 클래스의 프로퍼티와 메서드를 사용하기 위한 방법이다.
  - `as?` (옵셔널 캐스팅) : 변환이 성공하면 옵셔널 값을 가지며, 실패시에는 nil을 반환한다.
  - `as!` (강제 캐스팅) : 변환이 성공하면 언래핑된 값을 가지며, 실패시 런타임 에러가 발생한다.
  
  ## 업 캐스팅
  > 자식 클래스 -> 부모 클래스로 형변환 / 부모 클래스의 프로퍼티와 메서드를 사용하기 위한 방법이다.
  - `as` : 타입 변환이 확실하게 가능한 경우에만 사용한다. (그 외에는 컴파일 에러 발생)
  
</details>

<details>
  <summary> 열거형도 Hashable을 채택했을 때 자동으로 Hashable하게 만들 수 있나요? </summary>
  <br>
  
  - 열거형은 `associated value`가 없는 경우에는 `Hashable` 프로토콜만 채택해도 `Hashable`하게 사용할 수 있다.
  - 하지만 `associated valu`e가 있는 경우에는 `Hash 메서드`를 구현해주어야 한다.
  
</details>

<details>
<summary> cow란 무엇인가요? </summary>
<div markdown="1">
<br>
  
  ### Copy on Write
  > 컴퓨터 프로그래밍에서 복사 동작을 할 때, 실제 원본이나 복사본이 수정되기 전까지는 복사를 하지 않고 원본 리소스를 공유함 원본이나 복사본에서 수정이 일어날 경우, 그때 복사하는 작업을 함

  ### 작동 방식
  대표적으로 Swift에서 Array는 Value 타입이기 때문에, 값 복사가 일어나게 된다. 하지만, cow 때문에 처음에는 같은 메모리를 참조하고 있다가 어느 하나가 수정이 일어나게 되면 복사가 진행된다.
  
  ### 사용하는 이유
  일단 복사를 한다고 해서 꼭 수정이 일어나는 것은 아니다. 따라서, 불필요한 메모리 비용을 줄이기 위해 사용된다.

<summary>Enum 과 Struct 는 어떤 차이가 있는지?</summary>
<div markdown="1">
<br>
    - Enum 타입은 열거형 타입으로 연관된 값들의 집합이다. case 하나하나가 하나의 값을 나타내는 타입. 
    - Struct는 프로퍼티와 메서드로 구성된 타입. enum, struct 모두 class와 다르게 값타입이며, 상속이 불가능하지만 프로토콜 채택은 가능함.
  
</div>
</details>

<details>
<summary>Int / Int32 / Int64  | UInt / UInt32 / UInt64 각각의 차이는 무엇인지?</summary>
<div markdown="1">
<br>
    - 모두 정수를 나타내는 데이터 타입. 뒤에 붙는 32,64는 타입이 표현할 수 있는 비트의 크기. 
    - Int는 음수와 0, 양수를 표현할 수 있고, UInt는 양수만 표현할 수 있음. 
    - 크기가 표시되지 않은 Int, UInt는 해당 프로그램이 컴파일되는 컴퓨터의 시스템 아키텍처를 따른다. 즉, 자신이 사용하는 컴퓨터가 32비트 일 경우, Int의 범위는 -2^16 ~ 2^16 - 1 이고 64비트일 경우 -2^32 ~ 2^32 - 1 이다. 
    -UInt의 범위가 필요하지 않는 한 Int 사용 권장. 두 타입을 모두 사용하면 서로 다른 타입의 값을 교환할때 자원소모 크기 때문.
 
</div>
</details>

<details>
  <summary> closure를 이용한 stored property와 computed property의 차이점 </summary>
  <br>
  
  - Closure를 이용하여 프로퍼티를 세팅하게 되면 해당 프로퍼티가 처음 호출이 될 때 클로저 안의 코드가 수행되어 프로퍼티의 값이 정해지고, 정해지고 난 후에는 그 값이 계속 쓰인다.
  - Computed property는 해당 변수가 호출이 될 때마다 computed property의 block이 실행되어 값을 반환한다.
  
<summary>Any 와 AnyObject는 어떤것인지?</summary>
<div markdown="1">
<br>
    - Any는 함수타입을 포함하여 Swift의 모든 데이터 타입을 지칭하는 타입. Int, String 같은 기본 데이터 타입까지 포함. 
    - AnyObject는 모든 클래스 타입의 인스턴스를 나타내는 프로토콜임 (범위 : Any > AnyObject).
  
</div>
</details>
  
  
<details>
  <summary> Enumeration에 대해 설명해주세요 </summary>

## 열거형이란
> An enumeration defines a common type for a group of related values   
> and enables you to work with those values in a type-safe way within your code.

: 관련된 값으로 이루어진 그룹을 공통 타입으로 선언하여 `type-safety`를 보장하여 코드를 작성할 수 있게 해준다.

```swift
// enum 예시
enum CompassPoint {
    case north
    case south
    case east
    case west
}

// 콤마(,)를 사용해 한줄에 적을 수도 있다.
enum Planet {
    case mercury, venus, earch, mars, jupiter, saturn
}

// dot(.)을 통해 값에 접근할 수 있다.
let direction: CompassPoint = .south
```

- C나 Objective-C는 int값들로 열거형을 선언하는 반면 swift에서는 case값이 string, character integer, floating값들을 사용할 수 있다.
- 열거형은 1급 클래스형(first-class types)여서 연산프로퍼티 사용, 초기화 지정, 초기선언 확장이 가능하다.

## 열거형을 왜 쓰는가?
좋은 코드의 기준이 보기 쉬운 깔끔한 코드, 효율적인 코드 라고 한다.
```
열거형을 사용하면...
- 코드를 보다 깔끔하게 작성할 수 있다.
- 코드 작성 시 실수도 줄여준다.
```
## 열거형의 특징
### 1) `switch` 문과의 연계
- switch문과 연계하여 사용하면 좋다.
    - 반드시 열거형의 모든 case를 완전히 포함해야 한다.
```swift
switch direction {
    case .north:
        print("현재 북쪽으로 향하고 있습니다.")
    case .south:
        print("현재 남쪽으로 향하고 있습니다.")
    case .west:
        print("현재 서쪽으로 향하고 있습니다.")
    case .east:
        print("현재 동쪽으로 향하고 있습니다.")
}

// 만약 모든 케이스 처리를 기술하는게 적당하지 않다면 default를 작성할 수 있다.
let myPlanet: Planet = .earth

switch myPlanet {
    case .earth:
        print("나의 행성은 지구입니다.")
    default:
        print("외계 행성입니다. 왹왹")
}
```

### 2) 연관 값 (Associated Values)
- 각 `case`에 `custom type`의 추가적인 정보를 저장할 수 있다.
- Alamofire를 사용할 때 `let value`, `let error` 부분이 연관값의 예시
```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```

### 3) 원시값 (RawValue)
- case에 raw값을 지정할 수 있다.
- raw값은 `String`, `Character`, `Integer`, `Float` 을 사용할 수 있다.
    단, 각 원시값은 열거형 선언에서 유일해야 한다. (중복X)
- 암시적 할당이 가능하다.
// RawValue로 초기화가 가능하다. -> 존재하지 않는 값으로 초기화하면 `nil`이 된다.
```swift
enum Number: Int {
    case one = 1 // 명시적으로 1 선언
    case two // 암시적으로 2 할당
    case three // 암시적으로 3 할당
}

// RawValue로 초기화
let myNumber = Number(rawValue: 2) // two
```

### 4) `RawValue`와 `Associated Value`의 차이는?
- `rawValue`는 개별 `case`와 대응대는 값으로 다른 `case`와의 구분되는 유일한 값이다.
- `associated value`는 특정한 `case`와 연결되는 타입이다.
```
즉,   
rawValue의 경우 값이 다르면 다른 case에 해당하지만, 
associated value는 동일한 case 내에서 다른 값을 가질 수 있다.
```
  
</details>
