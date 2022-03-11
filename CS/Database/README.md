# Database


<details>
<summary> DB에서의 Commit과 Rollback이란? </summary>
<div markdown="1">
<br>

- 커밋(Commit): 모든 부분작업이 정상적으로 완료하면 이 변경사항을 한꺼번에 DB에 반영
    - 작성한 쿼리문에서 Update, Delete, Insert를 수행했을 때, 그 쿼리문 수행결과에 대해 확정을 짓겠다는 뜻이다.
- 롤백(Rollback): 부분 작업이 실패하면 트랜잭션 실행 전으로 되돌림
    - 쿼리문 수행결과에 대해 번복을 함. 즉, 쿼리문 수행 이전으로 원상복귀 하겠다는 뜻이다(Commit 하기 전에 사용됨).
  
</div>
</details>


<details>
<summary> 데이터베이스 뷰란? 장점과 단점은? </summary>
<div markdown="1">
<br>

> 데이터베이스 뷰란?
> 

허용된 데이터를 제한적으로 보여주기 위해 하나 이상의 테이블에서 유도된 가상 테이블입니다.

> 데이터베이스 뷰의 장점과 단점은 무엇입니까?
> 

장점

- 뷰의 데이터가 저장되는 물리적 위치가 없으므로 리소스를 낭비하지 않고 출력을 생성합니다.
- 삽입, 업데이트 및 삭제와 같은 명령을 허용하지 않으므로 데이터 액세스가 제한됩니다.

단점

- 해당 뷰와 관련된 테이블을 삭제하면 뷰가 관련이 없습니다.
- 큰 테이블에 대해 뷰를 만들 때 더 많은 메모리가 사용됩니다.
  
</div>
</details>



<details>
<summary> 교착상태란? 방지하기 위한 방법? </summary>
<div markdown="1">
<br>
  
  
> 교착상태란?
> 

2개 이상의 트랜잭션이 특정 자원(테이블 또는 행)의 잠금(Lock)을 획득한 채 다른 트랜잭션이 소유하고 있는 잠금을 요구하면 아무리 기다려도 상황이 바뀌지 않는 상태가 되는데 이를 **교착상태** 라고 합니다.

> 교착상태를 방지하기 위한 방법에 대해 설명하세요.
> 
  
- 트랜잭션을 자주 커밋한다.
- 정해진 순서로 테이블에 접근한다.
- SELECT ~ FOR UPDATE 의 사용을 피한다.
  
  
  
</div>
</details>

<details>
<summary> ACID는 각각 무엇을 일컫는 단어인가? 각각에 해당하는 설명을 해주세요. </summary>
<div markdown="1">
<br>
  
  
> ACID?
> 

- Atomacity(원자성)
- Consistency(일관성)
- Isolation(격리성)
- Durability(지속성)

> 각 특성에 대한 설명
> 
  
- Atomacity
    - 트랜잭션의 작업이 부분적으로 실행되거나 중단되지 않는 것을 보장하는 것을 말합니다.
    - All or Nothing의 개념으로서 작업 단위를 일부분만 실행하지 않는다는 것을 말합니다.
- Consisteny
    - 트랜잭션이 성공적으로 완료되면 일관적인 DB 상태를 유지하는 것을 말합니다.
    - 여기서 말하는 일관성이란, 기본 키, 외래 키 제약과 같은 명시적인 무결성 제약 조건들뿐만 아니라, 대표적인 자금 이체 예에서 두 계좌 잔고의 합은 이체 전후가 같아야 한다는 사항과 같은 비명시적인 일관성 조건들도 있습니다.
- Isolation
    - 여러 트랜잭션이 동시에 수행되더라도 각각의 트랜잭션은 다른 트랜잭션의 수행에 영향을 받지 않고 독립적으로 수행되어야 합니다.
- Durability
    - 트랜잭션이 성공적으로 완료되어 커밋되고 나면, 해당 트랜잭션에 의한 모든 변경은 향후에 어떤 소프트웨어나 하드웨어 장애가 발생되더라도 보존되어야 합니다.
  
</div>
</details>

<details>
<summary> Functional Dependency가 무엇인지, Fully Functional Dependency의 조건, Fully Functional Dependency의 이점 </summary>
<div markdown="1">
<br>
  
  
> Functional Dependency이란?
> 

함수와 같이 어떠한 값을 통해 종속 관계에 있는 다른 값을 유일하게 결정할 수 있다는 것입니다. 데이터베이스에서의 함수 종속성을 더욱 명확하게 정의하면 다음과 같습니다.

어떤 테이블 **R**에 존재하는 필드들의 부분집합을 각각 **X**와 **Y**라고 할 때, **X**의 한 값이 **Y**에 속한 오직 하나의 값에만 사상될 경우에 "**Y**는 **X**에 함수 종속 (**Y** is functionally dependent on **X**)"이라고 하며, **X**→**Y**라고 표기합니다.

> Fully Functional Dependency의 조건
> 

종속자(Dependant)가 기본키에만 종속되며, 기본키가 여러 속성으로 구성되어 있을경우 기본키를 구성하는 모든 속성이 포함된 기본키의 부분집합에 종속된 경우입니다.

> Fully Functional Dependency의 이점
> 

Data Anomaly를 예방할 수 있습니다.
  
</div>
</details>








