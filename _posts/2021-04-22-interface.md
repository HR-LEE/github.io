---
layout: post
title: "JAVA - Interface"
---

## 1. 인터페이스란?

인터페이스는 무엇인가?
* 어떠한 동일한 행위, 목적 등에 대하여 규칙, 규격, 약속 등을 정한 개념.   

* 예시 1) 우리나라에서는 전기 플러그와 콘센트를 모두 동일한 220V 규격을 사용한다.   
  - 220V의 전기를 사용하는 어떤 제품이던 우리나라 어디서든 콘센트가 존재하면 플러그를 꼽아서 사용할 수 있다.

* 예시 2) 컴퓨터 USB 단자에는 USB의 규격만 맞춘 제품.   
  - USB(저장장치)를 쓸 수도 있고, 스마트폰과 연결하여 충전 및 기타 동기화 등 많은 작업을 할 수 있다.   

* 위의 예시와 같이 인터페이스는 동일한 행위에 대한 규약(전기를 제공/받는 행위, USB단자를 통해 연결되는 행위)을 나타낸다.   
이런 동일한 행위에 규약이 없다면 콘센트에 맞는 별도의 제품을 찾아서 선택하고, 컴퓨터 케이스 모양에 맞는 USB를 찾는 등 번거로운 상황이 벌어졌을 것이다.


## 2. JAVA 인터페이스의 형태
```
interface printable {
  String newLine = "\n";
  void print(string s);
}
```

* 인터페이스는 변수와 함수를 갖을 수 있다.   
  - 변수: 변수를 선언 했을 시에는 값을 같이 정의해줘야한다.
  - 함수: 함수의 내용은 없고 함수명과 받는 파라미터만 정의내려야한다.

## 3. JAVA 인터페이스 사용

```
class Screen implements printable, touchable {
  public void print(String s) {
    //상속 받은 printable 인터페이스의 함수를 구현.
    System.out.println(s)
  }

  public void touch() {
    //상속 받은 touchable 인터페이스의 함수를 구현.
  }
}
```

* 인터페이스를 상속 받는 클래스는 인터페이스에 정의된 메서드의 내용(동작)을 구현해줘야한다.

* 클래스는 인터페이스를 여러개 상속 받을 수 있다.
  - 위의 코드를 보면 Screen Class는 printable 출력이 가능하고, touchable 터치가 가능하도록 두 가지의 인터페이스를 상속 받았다. (다중 상속 가능)   

```
Class Tablet {
  public static void main(String args[]) {
    
    // Tablet은 Screen을 갖고 있다.
    Screen screen = new Screen();
    screen.print("this is Screen!");
    screen.touch();

    // 출력기능만 사용할 수 있는 Screen
    printable print = new Screen();
    print.print("this is print function in Screen");
    // print.touch(); // Error 이 스크린은 touch 기능을 사용할 수 없다.

    // touch만 사용할 수 있는 Screen
    touchable touch = new Screen();
    touch.touch();
    // touch.print("I touched the screen"); // Error 이 스크린은 출력을 사용할 수 없다.

  }
}
```

* 인터페이스를 상속 받은 클래스는 클래스 자체로 데이터 타입으로 사용할 수도 있고, 상속 받은 인터페이스를 데이터 타입으로 사용할 수 있다.
  - 클래스가 다양한 형태로 사용될 수 있다. (다형성)
  - 클래스 내의 기능이 많아질 경우 필요한 기능이 있는 인터페이스 타입으로 정의하여 사용할 수 있다.

[참조] [생활코딩 - JAVA 인터페이스 강의.](https://youtu.be/d_9tbUQ5G7E)