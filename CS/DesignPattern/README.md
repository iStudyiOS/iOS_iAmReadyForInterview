# Design Pattern

<details>
  <summary> 디자인패턴이란 무엇이고, 왜 필요한가? </summary>
  <br>

- 객체 지향 프로그래밍은 40여년 전부터 현재까지도 사용되어지고 있으며, 선조 프로그래머들의 유지보수와 협업에 용이한 코드들의 구조에 대한 노하우가 쌓이게 되었다.
- 이 데이터들을 패턴화 한 것이 `디자인 패턴` 이다.
- 사용하는 이유는 
    - 문제를 접근하는 방법을 새로 만들어내는 것보다, 기존에 비슷한 상황에서 사용했던 템플릿을 활용하여 문제를 해결하면 능률적으로 일을 처리할 수 있다.
    - 협업 시, 언어에 구애 받지 않고 의사소통이 가능하며, 일관성 있는 코드를 작성할 수 있다.

- 대표적인 디자인 패턴으로는 `MVC, MVVM, MVP, VIPER` 등이 있다.

</details>


<details>
  <summary>의존성과 의존성 역전에 대하여</summary>
  <br>

  ## 의존성
  - 객체 지향 프로그래밍에서 Dependency, 의존성은 서로 다른 객체 사이에 의존 관계가 있다는 것을 말한다.
  - 즉, 의존하는 객체가 수정되면, 다른 객체도 영향을 받는다는 것

  ## 의존성 역전 법칙(Dependency Inversion Principle)
  - DIP, 의존 관계 역전 법칙은 객체 지향 프로그래밍 설계의 다섯가지 기본 원칙(SOLID) 중 하나
  - 구체적인 객체는 추상화된 객체에 의존 해야 한다는 것이 핵심
  - Swift에서 추상화된 객체는 Protocol

    ```swift
    protocol Menu {
        func printCoffee()
        func printMeal()
    }

    class Eat: Menu {
        var coffee: String
        var meal: String

        init(coffee: String, meal: String) {
            self.coffee = coffee
            self.meal = meal
        }

        func printCoffee() {
            print("아메리카노")
        }

        func printMeal() {
            print("피자")
        }
    }

    /* todayEat 변수는 추상적인 객체인 Menu타입에 의존
    여기서 changeMenu 함수를 활용해서 의존성 주입 */
    struct Person {
        var todayEat: Menu

        func printCoffee() {
            todayEat.printCoffee()
        }

        func printMeal() {
            todayEat.printMeal()
        }

        mutating func changeMenu(menu: Menu) {
            self.todayEat = menu
        }
    }
    /* Eat객체와 Person객체는 거의 독립적인 객체 */
    let menu = Eat(coffee: "아메리카노", meal: "피자")
    let anotherMenu = Eat(coffee: "라떼", meal: "햄버거")

    var suhshin = Person(todayEat: menu)

    suhshin.printCoffee()
    /* print 아메리카노 */
    suhshin.changeMenu(menu: anotherMenu)
    suhshin.printCoffee()
    /* print 라떼 */
    ```

</details>
<details>
  <summary>의존성 주입에 대하여</summary>
  <br>

  ## 의존성 주입(Dependency Injection)
  - 객체, class에 대한 프로토콜을 정의하고, 해당 프로토콜을 상속 받게 되는 객체, class를 통해 주입하는 개념
  - 언제 사용해야할지를 구체적으로 고민하고 구성
  - Unit Test가 용이, 코드의 재활용성 증대
  - 의존성(종속성)을 줄이고, 결합을 낮추면서 유연한 코드 작성이 가능

    ```swift
    @objc protocol Driving {
        func startDriving()
        func stopDriving()
        @objc optional func isDriving() -> Bool
    }

    class BMW: Driving {
        func startDriving() {
            print("start driving")
        }

        func stopDriving() {
            print("stop driving")
        }
    }

    class HYUNDAI: Driving {
        func startDriving() {
            print("start driving")
        }

        func stopDriving() {
            print("stop driving")
        }

        func isDriving() -> Bool {
            return true
        }
    }

    class SelectedCar {
        var car: Driving
        init(car: Driving) {
            self.car = car
        }
    }

    let selectedCar = SelectedCar(car: BMW())
    let selectedCar2 = SelectedCar(car: HYUNDAI())

    ```

</details>


