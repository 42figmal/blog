---
title: "생성자"
# weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
description: " "
date: "january 24, 2023"
categories: ["Programming", "Swift"]
---
# Initiallizer 생성자
- 클래스 안의 함수를 매서드라고 부르며, 매서드 중 클래스 안 저장 속성을 초기화하는 함수를 **생성자** 라고 부른다.
- 클래스가 품고있는 속성들이 많아질 경우 사용시 일일히 초기화하기 어렵기 때문에 우리는 초기화를 도와주는 생성자를 사용한다!
### init() 자동 구현
- 저장 속성의 기본값을 설정한 경우에는 스위프트에서 자동으로 `init`(생성자)를 구현해준다.
- 클래스로 인스턴스를 생성하는 `var buleCake = Cake()`는 사실 `var blueCake = Cake.init()`의 축약형.
```swift
class Cake {
    var name: String = "블루케이크"
    var subname: String = "블루베리케이크" 
//  여기 숨어있지롱  
//  init() {
//        
//  }
}
var buleCake = Cake()
```
### Self.
- 생성자가 파라미터로 받는 name과 price는 `self.name`를 초기화한다.  
- 생성자 내부의 `self.name`는 Cake 클래스를 이용해 만든 해당 객체의 `var name`에 담긴다.
- blueCake 선언 시 init은 파라미터로 전달받은 `name: "블루케이크"`로 `self.name`을 초기화한다. 이때 `self.name`은 곧 `blueCake.name`이다. 
### Overloading
- 생성자도 매서드이므로 Overloading을 지원하므로, 클래스 안에 생성자를 맘대로맘대로 열매 먹은 것 마냥 생성할 수 있다.
- 장점은 개발자가 인스턴스를 만들 때 선택의 폭이 넓어진다는점? 
```swift
class Cake {
    var name: String
    //var name: String?
    var subname: String

    // 여러 저장 속성에 한가지 입력값을 넣을 수도 있고
    init(name: String) {
        self.name = name
        self.subname = name
    }
    // 한번에 다 받을 수도 있다.
    init(name: String, subname: String, price: Double) {
        self.name = name
        self.subname = subname
        self.price = price
    }
}
```
##  Class Initiallizer 클래스 생성자
- 속성을 옵셔널로 선언하면 값이 없을경우 nil로 표현이 가능하므로 init을 사용할 필요가 없다.
### 1. Designated Initiallizer 지정 생성자
**지정 생성자는 모든 속성을 초기화 해야한다.**
일반적인 생성자를 지정 생성자라고 부르며, 그 범주 안에는 기본 생성자 `init()`도 포함되어있다.
### 2. Convenience Initiallizer 편의 생성자
**편의 생성자는 모든 속성을 초기화 할 필요가 없다.**
**편의 생성자는 상속되지 않으며, 서브클래스에서 재정의 할 수 없다.**
지정 생성자를 베이스로 만들어낸 바리에이션.
(편의)생성자 내에서 지정 생성자를 호출하는 것이 특징!
코드 중복을 없애 유지보수가 쉬워지며 특히 상속을 지원하는 클래스에선 저장 속성이 많아 실수가 나올 수 있는데 이를 방지해줌.
생성자 중복을 없애고 편의 생성자를 통해 지정 생성자를 호출해야한다!
```swift
struct Cake {
    let name, subname: String
    //편의 생성자
    convenience init() {
        self.init(name: "블루케이크", subname: "블루베리케이크")
    }
    //편의 생성자
    convenience init(name: String) {
        self.init(name: name, subname: name)
    }
    //지정 생성자
    init(name: String, subname: String) {
        self.name = name
        self.subname = subname
    }
}
```
### 3. 상속과 생성자
- 

1. 지정생성자를 선언한다. 이때, B클래스의 저장 속성인 var c를 설정해주어야함.
2. 그리고 super.init() 즉, 상위 클래스인 A에서 만든 지정생성자를 호출한다.
이 위의 두가지 기본 세팅이다. 자기 자신의 저장속성을 설정하고, 상위 클래스의 지정생성자를 호출하는 것.

클래스 A를 상속해 만들어진 클래스 B가 있다고 해보자.
B클래스에서 생성자를 활용하는 방법
```swift
class A {
    var a: Int
    var b: Int
    
    init(a: Int, b: Int) {
        self.a = a
        self.b = b
    }
    convenience init() {
        self.init(a: 0, b: 0)
    }
}
```

```swift
class B: A {
    var c: Int
    
    init(a: Int, b: Int, c: Int) {
        self.c = c
        //self.a = a 또는 self.b = b 처럼
        //이때 여기서 A의 저장속성에 접근하는 것은 불가능하다.
        //왜냐? 아직 상위 클래스 A의 생성자를 호출하지 않아서
        //해당 메모리 셋팅이 되기 전이기 때문이다.
        super.init(a: a, b: b) // 상위 지정 생성자 호출
        //이 밑으로는 이제 A의 저장 속성에 접근이 가능하다.
        //self.a = 0 등
        //메서드도 운용 가능함
    }
    con
}
```

##  구조체 생성자
구조체는 지정 생성자와 실패가능 생성자를 가질 수 있음.

### 1. 구조체 지정 생성자
다른 생성자를 호출하는 생성자를 선언하는 방식도 가능하다. 이 경우는 클래스에서 편의 생성자에 해당한다. 물론 구조체는 클래스와 달리 편의 생성자라는 개념이 없으니 그냥 지정 생성자임.
장점은 코드 중복을 방지. 전체적인 생성자를 하나 만들고, 다른 생성자에서 해당 생성자를 가져오는 그런 방법.
```swift
struct Cake {
    let name, subname: String
    
    init() {
        self.init(name: "블루케이크", subname: "블루베리케이크")
    }
    
    init(name: String) {
        self.init(name: name, subname: name)
    }
    
    init(name: String, subname: String, price: Double) {
        self.name = name
        self.subname = subname
        self.price = price
    }
}
var buleCake = Cake()
```

### Memberwise Initializer
구조체의 경우 맴버와이즈 이니셜라이저를 제공해줌. 생성자를 딱히 적지 않아도 xcode에서 알아서 구현해준다. 생성자를 당신이 새로 만들면 더 이상 안해줌...
이런 이유? 클래스보다 구조체를 더 많이 쓰니까 허들을 낮춰준게 아닐까?
```swift
struct Cake {
    var name: String
    var price: Double
//    여기 숨어있지롱 Xcode가 구현해주지롱.. 물론 당신이 새로 init을 생성하면 the end
//   init(name: String, subname: String, price: Double) {
//      self.name = name
//        self.subname = subname
//        self.price = price
//   }
}
//var blueCake = Cake(name: String, price: Double)
```