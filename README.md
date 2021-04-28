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
