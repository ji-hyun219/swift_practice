# swift_practice
swift 언어와 친해지기

```swift
let age: Int = 10
print("안녕하세요! 저는 \(age + 5) 살입니다")
```

```swift
class Person {
  var name: String = "yagom"
  var age: Int = 10
}

let yagom: Person = Person();
```
&nbsp;

***
### 상수, 변수
- `var` 변수 (차후에 다른 값 할당 가능)
- `let` 상수 (차후에 다른 값 할당 불가)  

&nbsp;
***

&nbsp;

### 기본 데이터 타입
주의 사항: swift 는 뛰어쓰기에 엄격하다.
&nbsp;
&nbsp;

1. UInt : 양의 정수 타입

```swift
var someInt: Int = -100
var someUInt: UInt = 100
someUInt = someInt // error
```


2. Float : 32비트 부동소수타입
```swift
var someFloat: Float = 3.14
someFloat = 3 // 정수를 넣어도 무리 없다
```


3. Double : 64비트 부동소수타입
```swift
var someDouble: Double = 3.14
someDouble = 3 // 정수 ok!
someDouble = someFloat // type error!
```

&nbsp;

4. Character   
한문자만 할당할 수 있다.   
고로, 문자열은 할당할 수 없다.


5. String : 문자열   
문자열 타입은 Charcter 타입 할당 불가능하다.

&nbsp;
***

### Any, AnyObject, nil
- `Any` : Swift 의 모든 타입을 지칭하는 키워드
- `AnyObject` : 모든 클래스 타입을 지칭하는 프로토콜
- `nil` : 없음을 의미하는 키워드




#### Any
```swift
var someAny: Any = 100
someAny = "어떤 타입도 수용 가능합니다"
someAny = 123.12

let someDouble: Double = someAny // error : 왜냐하면 Double 타입에 Any를 할당할 수 없다
 
```
&nbsp;


#### AnyObject
```swift
class SomeClass {}
var someAnyObject: AnyObject = SomeClass()
someAnyObject = 123.12 // error
```
&nbsp;


#### nil
```swift
someAny = nil // error
someAnyObject = nil // error
```

어떤 데이터 값이 들어올 수 있지만 빈 값은 할당될 수 없다!   



***
&nbsp;


### 컬렉션 타입
컬렉션 타입이란 여러 값들을 묶어서 하나로 표현하는 형
1. `Array` - 순서가 있는 리스트 컬렉션
2. `Dictionary` - 키와 값의 쌍으로 이루어진 컬렉션
3. `Set` - 순서가 없고, 멤버가 유일한 컬렉션


&nbsp;
#### Array
```swift
var integers: Array<Int> = Array<Int>() // 빈 Int Array 생성
integers.append(1)
integers.append(100)


integers.contains(100)
integers.remove(at: 0)
integers.removeLat()
integers.removeAll()
integers.count
```



- 아래 Array<Double> 와 [Double]는 동일한 표현
   
```swift
var doubles: Array<Double> = [Double]() // 빈 Dobule Array 생성

var strings: [String] = [String]() // 빈 String Array 생성

var character: [Character] = [] // 빈 Character Array 생성
```

- let 을 사용해서 Array 선언하면 불변 Array 이다.

&nbsp;


#### Dictionary

```swift
// key 가 String 타입이고 Value 가 Any 인 빈 Dictionary 생성
var anyDictionary: Dictionary<String, Any> = [String: Any]()

anyDictionary["someKey"] = "value" // 값 할당
anyDictionary["someKey"] = "value1" // 값 수정
```
&nbsp;

- 아래 두 줄은 같은 표현이다

```swift
anyDictionary.removeValue(forKey: "someKey")
anyDictionary["someKey"] = nil
```


```swift
let emptyDictionary: [String: String] = [:] // 변경 불가
let initializedDictionary: [String: String] = ["name": "yagom", "gender": "male"]


let someValue: String = initializedIdctionary["name"] //error
```
- 왜 안되는지 생각 -> 키에 해당하는 값이 있을 수도 있고 없을 수도 있어서 -> 옵셔널에서 배워볼 것임


&nbsp;

#### Set
```swift
var integerSet: Set<Int> = Set<Int>() // 빈 Int Set 생성

integerSet.insert(1) // 중복된 값이 넣어질 수 없음. 한번만 추가된다
integerSet.contains(1)
integerSet.remove(100)
integerSet.removeFirst()
integerSet.count
```
&nbsp;

- Set 은 합집합, 교집합 등 집합연산에 용이하다

```swift
let setA: Set<Int> = [1, 2, 3, 4, 5]
let setB: Set<Int> = [3, 4, 5, 6, 7]
let union: Set<Int> = setA.union(setB) // 합집합
let sortedUnion: [Int] = union.sorted() // 위를 정렬

let intersection: Set<Int> = setA.intersection(setB) // 교집합
let subtracting: Set<Int> = setA.subtracting(setB) // 차집합
```

&nbsp;
***
### 함수 기본

```swift
func sum(a: Int, b: Int) -> Int {
  return a + b
}


func printMyname(name: String) -> Void {
  print(name)
}


func printMyname(name: String) {
  print(name)
}

 
 
// 함수 호출
sum(a: 3, b: 5)
printMyName(name: "yagom") // yagom
```

&nbsp;

### 함수 고급
기본값을 갖는 매개변수는 매개변수 목록 중에 뒤쪽에 위치하는 것이 좋다!
```swift
func 함수이름(매개변수1이름: 매개변수1타입, 매개변수2이름: 매개변수2타입 = 기본값) -> 반환타입 {
  return 반환값
}
```
&nbsp;

#### `전달인자 레이블`
전달인자 레이블은 함수를 호출할 때 `매개변수의 역할을 좀 더 명확`하게 하거나 `함수 사용자의 입장에서 표현`하고자 할 때 사용한다

```swift
func 함수이름(전달인자레이블 매개변수1이름: 매개변수1타입, 전달인자레이블 매개변수2이름: 매개변수2타입 = 기본값) -> 반환타입 {
  return 반환값
}
```
예시를 보자

```swift
func greeting(to friend: String, from me: String) -> {
  print("Hello, \(friend)! I'm \(me)")
}
```
이것은

```swift
func greeting(friend: String, me: String) -> {
  print("Hello, \(friend)! I'm \(me)")
}
```
이것과 다른 함수이다.   
또한 함수를 호출할 때에는 `greeting(to: "haha", from: "yagom")` 이렇게 `전달인자 레이블을 사용`해야 한다.
그러나 내부에서는 매개변수 이름 friend, me 사용해야 하는거 헷갈리지 말자.

&nbsp;

#### `가변 매개변수`
1. 전달 받을 값의 개수를 알기 어려울 때
2. 가변 매개변수는 `함수당 하나`만 가질 수 있다
```swift
func sayHelloToFriends(me: String, friends: String...) -> String {
  return "Hello, \(friends)! I'm \(me)")
}

print(sayHelloToFriends(me: "jihyun", friends: "gaga", "nana", "nunu"))
// Hello, ["gaga", "nana", "nunu"]! I'm jihyun!
```

만약 아무런 값을 넣어주지 않고 싶다면


```swift
print(sayHelloToFriends(me: "jihyun", friends: [])) // error
print(sayHelloToFriends(me: "jihyun", friends: nil)) // error

print(sayHelloToFriends(me: "jihyun")) // ok!
// Hello []! I'm jihyun!
```

