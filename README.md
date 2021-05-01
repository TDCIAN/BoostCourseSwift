# BoostCourseSwift
https://www.boostcourse.org/mo122/joinLectures/38564


### 2단원 16강 클래스 vs 구조체 / 열거형

Class
- 전통적인 OOP 관점에서의 클래스
- 단일상속
- (인스턴스/타입) 메서드
- (인스턴스/타입) 프로퍼티
- 참조 타입 (중요)
- Apple 프레임워크의 대부분의 큰 뼈대는 모두 클래스로 구성

Struct
- C언어 등의 구조체보다 다양한 기능
- 상속 불가
- (인스턴스/타입) 메서드
- (인스턴스/타입) 프로퍼티
- 값 타입 (중요)
- Swift의 대부분의 큰 뼈대는 모두 구조체로 구성

Enum
- 다른 언어의 열거형과는 많이 다른 존재
- 상속 불가
- (인스턴스/타입) 메서드
- (인스턴스/타입) 연산 프로퍼티
- 값 타입
- Enumeration
- 유사한 종류의 여러 값을 유의미한 이름으로 한 곳에 모아 정의
  - 예) 요일, 상태값, 월(Month) 등
- 열거형 자체가 하나의 데이터 타입
- 열거형의 case 하나하나 전부 하나의 유의미한 값으로 취급
- 선언 키워드 - enum

클래스 vs 구조체/열거형
- 클래스는 참조타입이고, 열거형과 구조체는 값 타입이라는 것이 가장 큰 차이
- 클래스는 상속이 가능하지만, 열거형과 구조체는 상속이 불가능하다.

1. 값 타입과 참조 타입 비교
- 값 타입(Value Type): 데이터를 전달할 때 값을 복사하여 전달한다.
- 참조 타입(Reference Type): 데이터를 전달할 때 값의 메모리 위치를 전달한다.

```swift
struct ValueType {
  var property = 1
}
class ReferenceType {
  var property = 1
}

// 첫 번째 구조체 인스턴스
let firstStructInstance = ValueType()

// 두 번째 구조체 인스턴스에 첫 번째 인스턴스 값 복사
var secondStructInstance = firstStructInstance

// 두 번째 구조체 인스턴스 프로퍼티 값 수정
secondStructInstance.property = 2

/* 
두 번째 구조체 인스턴스는 첫 번째 구조체를 똑같이 복사한 별도의 인스턴스이기 때문에
두 번째 구조체 인스턴스의 프로퍼티 값을 변경해도 첫 번째 구조체 인스턴스의 프로퍼티 값에는 영향이 없다
*/
print("first struct instance property : \(firstStructInstance.property)")    // 1
print("second struct instance property : \(secondStructInstance.property)")  // 2

// 클래스 인스턴스 생성 후 첫 번째 참조 생성
let firstClassReference = ReferenceType()
// 두 번째 참조 변수에 첫 번째 참조 할당
let secondClassReference = firstClassReference
secondClassReference.property = 2

/* 
두 번째 클래스 참조는 첫 번째 클래스 인스턴스를 참조하기 때문에
두 번째 참조를 통해 인스턴스의 프로퍼티 값을 변경하면
첫 번째 클래스 인스턴스의 프로퍼티 값을 변경하게 됨
*/
print("first class reference property : \(firstClassReference.property)")    // 2
print("second class reference property : \(secondClassReference.property)")  // 2
```

2. 값 타입(구조체, 열거형)을 사용하는 경우
- 연관된 몇몇의 값들을 모아서 하나의 데이터 타입으로 표현하고 싶은 경우
- 다른 객체 또는 함수 등으로 전달될 때 참조가 아니라 복사(값 복사)할 경우
- 자신을 상속할 필요가 없거나, 다른 타입을 상속 받을 필요가 없는 경우

3. 스위프트에서의 사용
- 스위프트의 기본 데이터 타입은 모두 구조체로 구현되어 있다.
Data types in Swift
```swift
public struct Int
public struct Double
public struct String
public struct Dictionary<Key: Hashable, Value>
public struct Array<Element>
public struct Set<Element: Hashable>
```
- 스위프트는 구조체와 열거형 사용을 선호한다.
- Apple 프레임워크는 대부분 클래스를 사용한다.
- 구조체/클래스 선택과 사용은 개발자의 몫이다.


### 2단원 17강 클로저 기본

클로저 기본

1. 클로저
- 클로저는 실행가능한 코드 블럭
- 함수와 다르게 이름정의는 필요하지는 않지만, 매개변수 전달과 반환값이 존재할 수 있다는 점이 동일하다
- 함수는 이름이 있는 클로저이다
- 일급객체로 전달인자, 변수, 상수 등에 저장 및 전달이 가능하다

2. 기본 클로저 문법
- 클로저는 중괄호 {}로 감싸져있다
- 괄호를 이용해 파라미터를 정의한다
- ->를 이용해 반환 타입을 명시한다
- 'in' 키워드를 이용해 실행 코드와 분리한다

```swift
{ (매개변수 목록) -> 반환타입 in
  실행 코드
}
```

3. 클로저 사용
```swift
// sum이라는 상수에 클로저를 할당
let sum: (Int, Int) -> Int = {(a: Int, b: Int) in
  return a + b
}

let sumResult: Int = sum(1, 2)
print(sumResult) // 3
```

4. 함수의 전달인자로서의 클로저
- 클로저는 주로 함수의 전달인자로 많이 사용된다
- 함수 내부에서 원하는 코드블럭을 실행할 수 있다

```swift
let add: (Int, Int) -> Int
add = { (a: Int, b: Int) in
  return a + b
}

let substract: (Int, Int) -> Int
substract = { (a: Int, b: Int) in
  return a - b
}

let divide: (Int, Int) -> Int
divide = { (a: Int, b: Int) in
  return a / b
}

func calculate(a: Int, b: Int, method: (Int, Int) -> Int) -> Int {
  return method(a, b)
}

var calculated: Int
calculated = calculate(a: 50, b: 10, method: add)
print(calculated) // 60

calculated = calculated(a: 50, b: 10, method: substract)

print(calculated) // 40

calculated = calculated(a: 50, b: 10, method: divide)

print(calculated) // 5

// 따로 클로저를 상수/변수에 넣어 전달하지 않고, 함수를 호출할 때 클로저를 작성하여 전달할 수도 있습니다.
calculated = calculate(a: 50, b: 10, method: { (left: Int, right: Int) -> Int in
  return left * right
})

print(calculated) // 500
```

### 2단원 18강 클로저 고급

클로저 고급 - 다양한 클로저 표현

클로저는 아래 규칙을 통해 다양한 모습으로 표현될 수 있습니다.
1. 후행 클로저: 함수의 매개변수 마지막으로 전달되는 클로저는 후행클로저(trailing closure)로 함수 밖에 구현할 수 있습니다.
2. 반환타입 생략: 컴파일러가 클로저의 타입을 유추할 수 있는 경우 매개변수, 반환 타입을 생략할 수 있습니다.
3. 단축 인자 이름: 전달인자의 이름이 굳이 필요 없고, 컴파일러가 타입을 유추할 수 있는 경우 축약된 전달인자 이름($0, $1, $2, ...)을 사용할 수 있습니다.
4. 암시적 반환 표현: 반환 값이 있는 경우, 암시적으로 클로저의 맨 마지막 줄은 return 키워드를 생략하더라도 반환 값으로 취급합니다.

기본 클로저 표현

```swift
// 클로저를 매개변수로 갖는 함수 calculated(a: b: method:)와 결과값을 저장할 변수 result 선언
func calculate(a: Int, b: Int, method: (Int, Int) -> Int) -> Int {
  return method(a, b)
}
var result: Int

// 1. 후행 클로저
// 클로저가 함수의 마지막 전달인자일 때, 마지막 매개변수 이름을 생략한 후 함수 소괄호 외부에 클로저를 구현할 수 있습니다.
result = calculate(a: 10, b: 10) { (left: Int, right: Int) -> Int in
  return left + right
}

print(result) // 20

/*
2. 반환타입 생략
- calculate(a: b: method:)함수의 method 매개변수는 Int 타입을 반환할 것이라는 사실을 컴파일러도 알기 때문에 굳이 클로저에서 반환타입을 명시해주지 않아도 됩니다.
- 대신 in 키워드는 생략할 수 없습니다.
*/
result = calculate(a: 10, b: 10, method: { (left: Int, right: Int) in
  return left + right
})

print(result) // 20

// 후행클로저와 함께 사용할 수도 있습니다
result = calculate(a: 10, b: 10) {(left: Int, right: Int) in
  return left + right
}

print(result) // 20

/*
3. 단축 인자이름
- 클로저의 매개변수 이름이 굳이 불필요하다면 단축 인자이름을 활용할 수 있습니다.
- 단축 인자이름은 클로저의 매개변수의 순서대로 $0, $1, $2, ...처럼 표현합니다.
*/
result = calculate(a: 10, b: 10, method: {
  return $0 + $1
})

print(result) // 20

// 당연히 후행 클로저와 함께 사용할 수 있습니다
result = calculate(a: 10, b: 10) {
  return $0 + $1
}

print(result) // 20

/*
4. 암시적 반환 표현
- 클로저가 반환하는 값이 있다면 클로저의 마지막 줄의 결과값은 암시적으로 반환값으로 취급합니다.
*/
result = calculate(a: 10, b: 10) {
  $0 + $1
}
print(result) // 20

// 간결하게 한 줄로 표현해 줄 수도 있습니다
result = calculate(a: 10, b: 10) { $0 + $1 }

print(result) // 20

// 축악 전과 후 비교

// 축약 전
result = calculate(a: 10, b: 10, method: { (left: Int, right: Int) -> Int in
  return left + right
})

// 축약 후
result = calculate(a: 10, b: 10) { $0 + $1 }
print(result) // 20
```

* 너무 축약된 코드는 타인이 보거나, 시간이 지난 뒤에 볼 때 명시성이 떨어질 수 있으므로 적정선에서 축약하도록 합시다!


### 2단원 19강 프로퍼티

프로퍼티

1.프로퍼티의 종류
- 인스턴스 저장 프로퍼티
- 타입 저장 프로퍼티
- 인스턴스 연산 프로퍼티
- 타입 연산 프로퍼티
- 지연 저장 프로퍼티

2. 정의와 사용
- 프로퍼티는 구조체, 클래스, 열거형 내부에 구현할 수 있습니다
- 다만 열거형 내부에는 연산 프로퍼티만 구현할 수 있습니다
- 연산 프로퍼티는 var로만 선언할 수 있습니다
- 연산프로퍼티를 읽기 전용으로는 구현할 수 있지만, 쓰기 전용으로는 구현할 수 없습니다
- 읽기전용으로 구현하려면 get 블럭만 작성해주면 됩니다. 읽기전용은 get 블럭을 생략할 수 있습니다
- 읽기, 쓰기 모두 가능하게 하려면 get 블럭과 set 블럭을 모두 구현해주면 됩니다
- set 블럭에서 암시적 매개변수 newValue를 사용할 수 있습니다.


```swift
struct Student {
  // 인스턴스 저장 프로퍼티
  var name: String = ""
  var `class`: String = "Swift"
  var koreanAge: Int = 0
  
  // 인스턴스 연산 프로퍼티
  var westernAge: Int {
    get {
      return koreanAge - 1
    }
    set(inputValue) {
      koreanAge = inputValue + 1
    }
  }
  
  // 타입 저장 프로퍼티
  static var typeDescription: String = "학생"
  
  /*
  // 인스턴스 메서드
  func selfIntroduce() {
    print("저는 ₩(self.class)반 ₩(name)입니다")
  }
  */
  
  // 읽기전용 인스턴스 연산 프로퍼티
  // 간단히 위의 selfIntroduce() 메서드를 대체할 수 있습니다
  var selfIntroduction: String {
    get {
      return "저는 ₩(self.class)반 ₩(name)입니다"
    }
  }
  
  /*
  // 타입 메서드
  static func selfIntroduce() {
    print("학생타입입니다")
  }
  */
  
  // 읽기전용 타입 연산 프로퍼티
  // 읽기전용에서는 get을 생략할 수 있습니다
  static var selfIntrodction: String {
    return "학생타입입니다"
  }
}

// 타입 연산 프로퍼티 사용
print(Student.selfIntroduction)
// 학생타입입니다

// 인스턴스 생성
var yagom: Student = Student()
yagom.koreanAge = 10

// 인스턴스 저장 프로퍼티 사용
yagom.name = "yagom"
print(yagom.name)
// yagom

// 인스턴스 연산 프로퍼티 사용
print(yagom.selfIntroduction)
// 저는 Swift반 yagom입니다

print("제 한국나이는 ₩(yagom.koreanAge)살이고, 미쿡나이는 ₩(yagom.westernAge)살입니다.")
// 제 한국나이는 10살이고, 미쿡나이는 9살입니다.
```

3. 응용
```swift
struct Money {
  var currentRate: Double = 1100
  var dollar: Double = 0
  var won: Double {
    get {
      return dollar * currencyRate
    }
    set {
      dollar = newValue / currencyRate
    }
  }
}

var moneyInMyPocket = Money()
moneyInMyPocket.won = 11000

print(moneyInMyPocket.won)
// 11000

moneyInMyPocket.dollar = 10
print(moneyInMyPocket.won)
// 11000
```

4. 지역변수 및 전역변수
- 저장 프로퍼티와 연산 프로퍼티의 기능은 함수, 메서드, 클로저, 타입 등의 외부에 위치한 지역/전역 변수에도 모두 사용 가능합니다.
```swift
var a: Int = 100
var b: Int = 200
var sum: Int {
  return a + b
}
print(sum) // 300
```

### 2단원 20강 프로퍼티 감시자

프로퍼티 감시자

1. 프로퍼티 감시자
- 프로퍼티 감시자를 사용하면 프로퍼티의 값이 변경될 때 원하는 동작을 수행할 수 있습니다.
- 값이 변경되기 직전에 willSet 블럭이, 값이 변경된 직후에 didSet 블럭이 호출됩니다.
- 둘 중 필요한 하나만 구현해 주어도 무관합니다.
- 변경되려는 값이 기존 값과 똑같더라도 프로퍼티 감시자는 항상 동작합니다.
- willSet 블럭에서는 암시적 매개변수 newValue를, didSet 블럭에서는 oldValue를 사용할 수 있습니다.
- 프로퍼티 감시자는 연산 프로퍼티에는 사용할 수 없습니다.
- 프로퍼티 감시자는 함수, 메서드, 클로저, 타입 등의 지역/전역 변수에 모두 사용 가능합니다.

2. 정의 및 사용
```swift
struct Money {
  // 프로퍼티 감시자 사용
  var currencyRate: Double = 1100 {
    willSet(newRate) {
      print("환율이 ₩(currenyRate)에서 ₩(newRate)으로 변경될 예정입니다"
    }
    
    didSet(oldRate) {
      print("환율이 ₩(oldRate)에서 ₩(currencyRate)으로 변경되었습니다")
    }
  }
  
  // 프로퍼티 감시자 사용
  var dollar: Double = 0 {
    // willSet의 암시적 매개변수 이름 newValue
    willSet {
      print("₩(dollar)달러에서 ₩(newValue)달러로 변경될 예정입니다")
    }
    
    // didSet의 암시적 매개변수 이름 oldValue
    didSet {
      print("₩(oldValue)달러에서 ₩(dollar)달러로 변경되었습니다"
    }
  }
  
  // 연산 프로퍼티
  var won: Double {
    get {
      return dollar * currencyRate
    }
    set {
      dollar = newValue / currencyRate
    }
    
    // 프로퍼티 감시자와 연산 프로퍼티 기능을 동시에 사용할 수 없습니다
  }
  
  var moneyInMyPocket: Money = Money()
  
  // 환율이 1100.0에서 1150.0으로 변경될 예정입니다
  moneyInMyPocket.currencyRate = 1150
  // 환율이 1100.0에서 1150.0으로 변경되었습니다
  
  // 0.0달러에서 10.0달러로 변경될 예정입니다
  moneyInMyPocket.dollar = 10
  // 0.0달러에서 10.0달러로 변경되었습니다
  
  print(moneyInMyPocket.won)
  // 11500.0
}
```

### 2단원 22강 인스턴스의 생성과 소멸(init / deinit)

인스턴스를 생성하는 이니셜라이저와 클래스의 인스턴스가 소멸될 때 호출되는 디이니셜라이저, 그리고 이와 관련된 것들에 대해 알아봅시다.
- 프로퍼티 초기값
- 이니셜라이저 init
- 디이니셜라이저 deinit

1. 프로퍼티 초기값
- 스위프트의 모든 인스턴스는 초기화와 동시에 모든 프로퍼티에 유효한 값이 할당되어 있어야 합니다.
- 프로퍼티에 미리 기본값을 할당해두면 인스턴스가 생성됨과 동시에 초기값을 지니게 됩니다.

```swift
class PersonA {
  // 모든 저장 프로퍼티에 기본값 할당
  var name: String = "unknown"
  var age: Int = 0
  var nickName: String = "nick"
}

// 인스턴스 생성
let jason: PersonA = PersonA()

// 기본값이 인스턴스가 지녀야 할 값과 맞지 않다면 생성된 인스턴스의 프로퍼티에 각각 값 할당
jason.name = "jason"
jason.age = 30
jason.nickName = "j"
```

2-1. 이니셜라이저(initializer)
- 프로퍼티 초기값을 지정하기 어려운 경우에는 이니셜라이저 init을 통해 인스턴스가 가져야 할 초기값을 전달할 수 있습니다.
```swift
class PersonB {
  var name: String
  var age: Int
  var nickName: String
  
  // 이니셜라이저
  init(name: String, age: Int, nickName: String) {
    self.name = name
    self.age = age
    self.nickName = nickName
  }
}

let hana: PersonB = PersonB(name: "hana", age: 20, nickName: "하나")
```

프로퍼티의 초기값이 꼭 필요 없을 때
- 옵셔널을 사용
- class 내부의 init을 사용할 때는 convenience 키워드 사용

```swift
class PersonC {
  var name: String
  var age: Int
  var nickName: String?
  
  init(name: String, age: Int, nickName: String) {
    self.name = name
    self.age = age
    self.nickName = nickName
  }
  
  // 위와 동일한 기능 수행
//  convenience init(name: String, age: Int, nickName: String) {
//    init(name: name, age: age)
//    self.nickName = nickName
//  }

  init(name: String, age: Int) {
    self.name = name
    self.age = age
  }
}

let jenny: PersonC = PersonC(name: "jenny", age: 10)
let mike: PersonC = PersonC(name: "mike", age: 15, nickName: "m")
```

암시적 추출 옵셔널은 인스턴스 사용에 꼭 필요하지만 초기값을 할당하지 않고자 할 때 사용
```swift
class Puppy {
  var name: String
  var owner: PersonC!
  
  init(name: String) {
    self.name = name
  }
  
  func goOut() {
    print("₩(name)가 주인 ₩(owner.name)와 산책을 합니다")
  }
}

let happy: Puppy = Puppy(name: "happy")
// 강아지는 주인없이 산책하면 안돼요!
// happy.goOut() // 주인이 없는 상태라 오류 발생
happy.owner = jenny
happy.goOut()
// happy가 주인 jenny와 산책을 합니다
```

2-2. 실패 가능한 이니셜라이저
- 이니셜라이저 매개변수로 전달되는 초기값이 잘못된 경우 인스턴스 생성에 실패할 수 있습니다.
- 인스턴스 생성에 실패하면 nil을 반환합니다.
- 실패가능한 이니셜라이저의 반환타입은 옵셔널 타입입니다.
- init?을 사용합니다.

```swift
class PersonD {
  var name: String
  var age: Int
  var nickName: String?
  
  init?(name: String, age: Int) {
    if (0...120).contains(age) == false {
      return nil
    }
    
    if name.characters.count == 0 {
      return nil
    }
    
    self.name = name
    self.age = age
  }
}

// let john: PersonD = PersonD(name: "john", age: 23)
let john: PersonD? = PersonD(name: "john", age: 23)
let joker: PersonD? = PersonD(name: "joker", age: 123)
let batman: PersonD? = PersonD(name:"", age: 10)

print(joker) // nil
print(batman) // nil
```

3. 디이니셜라이저(deinitializer)
- deinit은 클래스의 인스턴스가 메모리에서 해제되는 시점에 호출됩니다.
- 인스턴스가 해제되는 시점에 해야할 일을 구현할 수 있습니다.
- deinit은 매개변수를 지닐 수 없습니다.
- 자동으로 호출되므로 직접 호출할 수 없습니다.
- 디이니셜라이저는 클래스 타입에만 구현할 수 있습니다.
- 인스턴스가 메모리에서 해제되는 시점은 ARC(Auto Reference Counting)의 규칙에 따라 결정됩니다.

```swift
class PersonE {
  var name: String
  var pet: Puppy?
  var child: PersonC
  
  init(name: String, child: PersonC) {
    self.name = name
    self.child = child
  }
  
  // 인스턴스가 메모리에서 해제되는 시점에 자동 호출
  deinit {
    if let petName = pet?.name {
      print("₩(name)가 ₩(child.name)에게 ₩(petName)를 인도합니다")
      self.pet?.owner = child
    }
  }
}
var donald: Person#? = PersonE(name: "donald", child: jenny)
donald?.pet = happy
donal = nil // donald 인스턴스가 더이상 필요 없으므로 메모리에서 해제됩니다
// donald가 jenny에게 happy를 인도합니다

```

### 2단원 26강 프로토콜

1. 프로토콜
- 프로토콜은 특정 역할을 수행하기 위한 메서드, 프로퍼티, 기타 요구사항 등의 청사진을 정의합니다
- 구조체, 클래스, 열거형은 프로토콜을 채택(Adopted) 해서 특정 기능을 수행하기 위한 프로토콜의 요구사항을 실제로 구현할 수 있습니다
- 어떤 프로토콜의 요구사항을 모두 따르는 타입은 그 프로토콜을 준수한다(Conform)고 표현합니다
- 타입에서 프로토콜의 요구사항을 충족시키려면 프로토콜이 제시하는 청사진의 기능을 모두 구현해야 합니다.
  즉, 프로토콜은 기능을 정의하고 제시할 뿐이지 스스로 기능을 구현하지는 않습니다.
  
2. 정의
- protocol 키워드를 사용하여 정의합니다.
```swift
protocol 프로토콜이름 {
  // 정의부
}
```

3. 구현
<<프로퍼티 요구>>
- 프로퍼티 요구는 항상 var 키워드를 사용합니다
- get은 읽기만 가능해도 상관 없다는 뜻이며, get과 set을 모두 명시하면 읽기 쓰기 모두 가능한 프로퍼티여야 합니다
```swift
protocol Talkable {
  // 프로퍼티 요구
  var topic: String { get set }
  var language: String { get }
  
  // 메서드 요구
  func talk()
  
  // 이니셜라이저 요구
  init(topic: String, language: String)
}
```

3. 프로토콜 채택 및 준수
<<프로토콜 채택>>
- 타입명: 프로토콜 이름
```swift
// Person 구조체는 Talkable 프로토콜을 채택했습니다
struct Person: Talkable {
  // 프로퍼티 요구 준수
  var topic: String
  let language: String
  
  // 읽기전용 프로퍼티 요구는 연산 프로퍼티로 대체가 가능합니다
  var language: String { return "한국어" }
  
  // 물론 읽기, 쓰기 프로퍼티도 연산 프로퍼티로 대체할 수 있습니다
  var subject: String = ""
  var topic: String {
    set {
      self.subject = newValue
    }
    get {
      return self.subject
    }
  }
  
  // 메서드 요구 준수
  func talk() {
    print("₩(topic)에 대해 ₩(language)로 말합니다"
  }
  
  // 이니셜라이저 요구 준수
  init(topic: String, language: String) {
    self.topic = topic
    self.language = language
  }
}
```

프로퍼티 요구는 다양한 방법으로 해석, 구현할 수 있습니다.
```swift
struct Person: Talkable {
  var subject: String = ""
  
  // 프로퍼티 요구는 연산 프로퍼티로 대체가 가능합니다
  var topic: String {
    set {
      self.subject = newValue
    }
    get {
      return self.subject
    }
  }
  
  var language: String { return "한국어" }
  
  func talk() {
    print("₩(topic)에 대해 ₩(language)로 말합니다")
  }
  
  init(topic: String, language: String) {
    self.topic = topic
  }
}
```

4. 프로토콜 상속
- 프로토콜은 하나 이상의 프로토콜을 상속받아 기존 프로토콜의 요구사항보다 더 많은 요구사항을 추가할 수 있습니다
- 프로토콜 상속 문법은 클래스의 상속 문법과 유사하지만, 프로토콜은 클래스와 다르게 다중상속이 가능합니다
```swift
protocol 프로토콜 이름: 프로토콜 이름 목록 {
  // 정의부
}
```
```swift
protocol Readable {
  func read()
}

protocol Writeable {
  func write()
}

protocol ReadSpeakable: Readable {
  func speak()
}

protocol ReadWriteSpeakable: Readable, Writeable {
  func speak()
}

struct SomeType: ReadWriteSpeakable {
  func read() {
    print("Read")
  }
  
  func write() {
    print("Write")
  }
  
  func speak() {
    print("Speak")
  }
}
```

<<클래스 상속과 프로토콜>>
- 클래스에서 상속과 프로토콜 채택을 동시에 하려면 상속받으려는 클래스를 먼저 명시하고 그 뒤에 채택할 프로토콜 목록을 작성합니다
```swift
class SuperClass: Readable {
  func read()
}

class SubClass: SuperClass, Writeable, ReadSpeakable {
  func write() {}
  func speak() {}
}
```

5. 프로토콜 준수 확인
- is, as 연산자를 사용해서 인스턴스가 특정 프로토콜을 준수하는지 확인할 수 있습니다
```swift
let sup: SuperClass = SuperClass()
let sub: SubClass = SubClass()

var someAny: Any = sup
someAny is Readable // true
someAny is ReadSpeakable // false 

someAny = sub
someAny is Readable // true
someAny is ReadSpeakable // true

someAny = sup

if let someReadable: Readable = someAny as? Readable {
  someReadable.read()
} // read

if let someReadSpeakable: ReadSpeakable = someAny as? ReadSpeakable {
  someReadSpeakable.speak()
} // 동작하지 않음

someAny = sub

if let someReadable: Readable = someAny as? Readable {
  someReadable.read()
} // read
```


### 3단원 29강 고차함수

1.고차함수
- 고차 함수(Higher-order function)는 '다른 함수를 전달인자로 받거나 함수실행의 결과를 함수로 반환하는 함수'를 뜻합니다.
- 스위프트의 함수(클로저)는 일급시민(일급객체)이기 때문에 함수의 전달인자로 전달할 수 있으며, 함수의 결과값으로 반환할 수 있습니다.
- map, filter, reduce 함수는 스위프트 표준 라이브러리의 컨테이너 타입(Array, Set, Dictionary 등)에 구현되어 있습니다.

2. map
- map 함수는 컨테이너 내부의 기존 데이터를 변형(transform)하여 새로운 컨테이너를 생성합니다.

```swift
// 변형하고자 하는 numbers와 변형 결과를 받을 doubledNumbers, strings

let numbers: [Int] = [0, 1, 2, 3, 4]
var doubledNumbers: [Int]
var string: [String]
```
<< 기존의 for 구문 사용>>
```swift
doubledNumbers = [Int]()
strings = [String]()

for number in numbers {
  doubledNumbers.append(number * 2)
  strings.append("₩(number)")
}

print(doubledNumbers) // [0, 2, 4, 6, 8]
print(strings) // ["0", "1", "2", "3", "4"]
```

<<map 메서드 사용>>
```swift
// numbers의 각 요소를 2배하여 새로운 배열 반환
doubledNumbers = numbers.map({ (number: Int) -> Int in
  return number * 2
})

// numbers의 각 요소를 문자열로 변환하여 새로운 배열 반환
strings = numbers.map({ (number: Int) -> String in
  return "₩(number)"
})

print(doubledNumbers) // [0, 2, 4, 6, 8]
print(strings) // ["0", "1", "2", "3", "4"]

// 매개변수, 반환 타입, 반환 키워드(return) 생략, 후행 클로저
doubledNumbers = numbers.map { $0 * 2 }
print(doubledNumbers) // [0, 2, 4, 6, 8]
```

3. filter
- filter 함수는 컨테이너 내부의 값을 걸러서 새로운 컨테이너로 추출합니다.
<< 기존의 for 구문 사용 >>
```swift
// 변수 사용에 주목하세요
var filtered: [Int] = [Int]()

for number in numbers {
  if number % 2 == 0 {
    filtered.append(number)
  }
}

print(filtered) // [0, 2, 4]
```
<<filter 메서드 사용>>
```swift
// numbers의 요소 중 짝수를 걸러내어 새로운 배열로 반환
let evenNumbers: [Int] = numbers.filter {(number: Int) -> Bool in
  return number % 2 == 0
}
print(evenNumbers) // [0, 2, 4]

// 매개변수, 반환 타입, 반환 키워드(return) 생략, 후행 클로저
let oddNumbers: [Int] = numbers.filter {
  $0 % 2 != 0
}
print(oddNumbers) // [1, 3]
```
4. reduce
- reduce 함수는 컨테이너 내부의 콘텐츠를 하나로 통합합니다.
```swift
// 통합하고자 하는 someNumbers
let someNumbers: [Int] = [2, 8, 15]
```
<<기존의 for 구문 사용>>
```swift
// 변수 사용에 주목하세요
var result: Int = 0

// someNumbers의 모든 요소를 더합니다.
for number in someNumbers {
  result += number
}
print(result) // 25
```
<<reduce 메서드 사용>>
```swift
// 초깃값이 0이고 someNumbers 내부의 모든 값을 더합니다.
let sum: Int = someNumbers.reduce(0, { (first: Int, second: Int) -> Int in
  //print("₩(first) + ₩(second)") // 어떻게 동작하는지 확인해보세요
  return first + second
})
print(sum) // 25

// 초깃값이 0이고 someNumbers 내부의 모든 값을 뺍니다.
var subtract: Int = someNumbers.reduce(0, {(first: Int, second: Int) -> Int in
  //print("₩(first) - ₩(second)") // 어떻게 동작하는지 확인해보세요
  return first - second
})
print(subtract) // -25

// 초깃값이 3이고 someNumbers 내부의 모든 값을 더합니다.
let sumFromThree = someNumbers.reduce(3) { $0 + $1 }
print(sumFromThree) // 28
```

### 3단원 30강 더 알아보기

추가적으로 알아가야 할 문법과 개념들
- 제네릭(Generics)
- 서브스크립트(Subscript)
- 접근수준(Access Control)
- ARC(Automatic Reference Counting)
- 중첩타입(Nested Types)
- 사용자정의 연산자(Custom Operators)
- 오류 처리(Error Handling)
- 불명확 타입(Opaque Types)
- 프로토콜 지향 프로그래밍(Protocol Oriented Programming)
