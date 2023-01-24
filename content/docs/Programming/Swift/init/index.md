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
# 생성자
## Class-Object-Instance
- Class - 객체의 설계도
- Object - Class로 만들어낸 실체, 모든 Instance를 포괄하는 의미
## Init
클래스 안의 함수를 매서드라고 부른다.
매서드 중 클래스내 변수를 초기화하는 함수를 **생성자** 라고 부른다.

클래스가 품고있는 속성들이 많아질 경우
사용시 일일히 초기화하기 어렵기 때문에 우리는 초기화를 도와주는 생성자를 사용한다!

```swift
class Cake {
    var name: String
    var price: Double

    init(a:String, b:Double) {
        name = a
        price = b
    }
}

// 생성자 미사용 시
var blueCake = Cake()
blueCake.name = "블루케이크"
blueCake.price = 4.0

// 생성자 사용 시
var blueCake = Cake(a: "블루케이크", b: 4.0)
```

## Self.
  생성자가 파라미터로 받는 name과 price는 `self.name`를 초기화한다.  
  생성자 내부의 `self.name`는 Cake 클래스를 이용해 만든 해당 객체의 `var name`에 담긴다.
```swift
class Cake {
    var name: String
    var price: Double

    init(name:String) {
        self.name = name
        self.price = price
    }
}

var blueCake = Cake(name: "블루케이크")
blueCake.name //블루케이크
```
blueCake 선언 시 init은 파라미터로 전달받은 `name: "블루케이크"`로 `self.name`을 초기화한다.  
이때 `self.name`은 곧 `blueCake.name`이다.