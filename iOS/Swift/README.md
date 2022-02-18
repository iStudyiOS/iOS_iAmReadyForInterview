# Swift

<details>
<summary> mutating 키워드가 무엇인가요? </summary>
<div markdown="1">

스위프트에서 클래스는 레퍼런스 타입이고 구조체와 열거형은 값 타입이다.

값 타입은 기본적으로 인스턴스 메소드에서 내부 데이터를 수정할 수가 없다.

값 타입의 속성을 수정하려면 인스턴스 메서드에서 mutating 키워드를 사용해야 한다.

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

스위프트에서 모든 데이터타입(Int, Double, Set, Array, Dictionary 등등)은 모두 구조체 기반으로 구현되어있다. 구조체 기반이기 때문에 값타입이다. 열거형은 값타입이다.

클래스와 클로저(함수)는 참조타입이다.

</div>
</details>