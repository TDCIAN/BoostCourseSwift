# BoostCourseSwift
https://www.boostcourse.org/mo122/joinLectures/38564


### 2단원 16강 클래스 vs 구조체 / 열거형

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

2. 값 
```
