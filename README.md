# iOS_iAmReadyForInterview

### About
- iOS 면접 대비하여 CS와 iOS/Swift 전반적인 질문과 답변을 정리하는 레포입니다.
- 매주 스터디할 면접주제를 정하고 스터디원들이 정한 주제에 맞는 질문으로 모의면접을 진행합니다.
- 매주 스터디 미팅(화요일)에 진행한 자료들로 업로드 합니다. 

### Study Rule
1. 매주 스터디할 면접주제에 맞는 질문을 각자 3개를 [노션](https://www.notion.so/iOS_iAmReadyForInterview-b68e1a7178f84850b81f6f0260c56e75)에 업로드 합니다. 
2. 스터디전까지 취합된 질문에 대한 답을 공부해옵니다.
3. 스터디가 끝난 후 자신이 준비한 질문(꼬리질문도 포함)을 노션과 깃헙에 수정 및 업로드합니다.
4. 자신의 레포에 `fork`하여, 작성한 질문 내용에 대해 작성한 `Pull Request`를 날리고 `Merge`합니다.
```
// Pull Request 양식

Swift에 다음 세가지 질문을 작성하였습니다.

- [x] 옵셔널이란 무엇이고, 옵셔널 추출 방법에 대해 설명해주세요.
- [x] 클래스와 구조체는 언제 사용하면 좋은가요?
- [x] Any와 AnyObject는 무엇인가요?
```


###	Document Structure
```
├─CS
│  ├─READ.md(과목 링크)
│  ├─Network
│  ├─Database
│  ├─DesignPattern
│  ├─DataStructure
│  ├─Algorithm
│  ├─OperatingSystem
├─iOS
│  ├─READ.md(과목 링크)
│  ├─iOS
│  ├─Swift
├─SoftwareEngineering
│  ├─READ.md(개발상식)
```

### How to contribute
- 자신의 질문과 맞는 유형이름의 폴더안 md파일에 질문을 정리합니다.
- 필요시 헤더와 같은 마크다운 문법을 사용해서 소주제를 나누셔도 됩니다.
- 질문은 토글을 사용합니다.

#### 토글 사용법

```html
<details>
<summary>질문!</summary>
<div markdown="1">
<br>
    - 답!

    ### 공식문서에 따른 인용구가 있다면
    > 이것은 인용구 입니다.

    ### 예시코드
    ```swift
    var ios: String = "너무 재밌다. 하하"
    ```
</div>
</details>
```

<details>
<summary>질문!</summary>
<br>
  - 답!
  
  ### 공식문서에 따른 인용구가 있다면
  > 이것은 인용구 입니다.
  
  ### 예시코드
  ```swift
  var ios: String = "너무 재밌다. 하하"
  ```
</details>

#### Commit 규칙
- 새로운 질문 최초 추가 시
```
[ADD] 질문이름
```
- 이미 추가한 질문 내용 수정 시
```
[UPDATE] 질문이름
```
- 해당 질문 삭제 시
```
[DEL] 질문이름
```
- 삭제된 질문을 재업로드 시
```
[RE] 질문이름
```

<br>


## Link

### :point_right: [질문 리스트 노션링크](https://www.notion.so/iOS_iAmReadyForInterview-b68e1a7178f84850b81f6f0260c56e75)

### :one: [Algorithm](./CS/Algorithm/README.md)
### :two: [Database](./CS/Database/README.md)
### :three: [Data Structure](./CS/DataStructure/README.md)
### :four: [Design Pattern](./CS/DesignPattern/README.md)
### :five: [Network](./CS/Network/README.md)
### :six: [Operating System](./CS/OperatingSystem/README.md)
### :seven: [Algorithm](./CS/Algorithm/README.md)
### :eight: [iOS](./iOS/iOS/README.md)
### :nine: [Swift](./iOS/Swift/README.md)
### :zero: [Software Engineering](./SoftwareEngineering/README.md)

<br>
<hr>

### Reference
<details>
<summary>CS</summary>
<div markdown="1">

- https://mfamcs.netlify.app/docs/intro
- https://gyoogle.dev/blog/
- https://github.com/JaeYeopHan/Interview_Question_for_Beginner


</div>
</details>
<details>
<summary>iOS</summary>
<div markdown="1">

- https://github.com/JeaSungLEE/iOSInterviewquestions
- https://github.com/dev-yong/iOS-Programming-Reference#OOP
- https://github.com/giftbott/iOSDevLinks


</div>
</details>

