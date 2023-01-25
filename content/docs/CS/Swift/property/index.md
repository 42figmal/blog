---
title: "여러가지 속성"
# weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
description: "속성"
date: "january 25, 2023"
categories: ["Programming", "Swift"]
---
# Property
## 저장속성
메모리 공간을 가지고 값을 저장할 수 있는 속성이다.  
Class Cake의 저장속성은 `var name`, `var price` !
```swift
class Cake {
    var name: String
    lazy var price: Double = 0.1

    init (a:String) {
        name = a
    }
}
```
 
## 지연저장속성(Lazy Stored Properties)
속성의 초기화를 지연시키는 것으로, 해당 속성은 제외한 상태로 진행하다가 후에 접근 시 초기화하는 것이다.  
나중에 변화가 생기는 것이므로 `var` 로 선언해야며 미리 초기화 해두어야하는 것이 포인트!
메모리 관리를 위해
ㅈ
```swift
lazy var price: Double = 0.1
```