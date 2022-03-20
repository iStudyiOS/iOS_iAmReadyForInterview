# Design Pattern
<details>
  <summary>의존성과 의존성 역전에 대하여</summary>
  <br>
  ## 의존성 주입(Dependency Injection)
  - 객체, class에 대한 프로토콜을 정의하고, 해당 프로토콜을 상속 받게 되는 객체, class를 통해 주입하는 개념
  - 언제 사용해야할지를 구체적으로 고민하고 구성
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
