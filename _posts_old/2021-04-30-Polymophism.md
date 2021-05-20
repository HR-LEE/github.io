---
layout: post
title: "JAVA - 다형성(Polymophism)"
---

## 1. 다형성이란?

* 하나의 객체가 '여러 가지 형태(타입)를 가질 수 있는 성격'을 의미한다.
* 하나의 사물(객체)을 다양한 형태(타입)으로 선언하고 그 형태에 맞는 성격을 나타낸다. 하나의 객체가 한개의 분류로 나뉠 수도 있지만, 여러개의 분류(성격, 성향) 등을 갖고 있을 수 있다.

* 예시 1) 동물 중에 육식성 포유류 분류들은 식육목으로 분류하는 계통이 있고, 포유강 계열로 분류하는는 계통이 있다. 이런 육식동물은 분류에 따라서 성향 및 특징을 나타낼 수 있다.


## 2. JAVA에서의 다형성

* Java에서 다형성은 클래스 혹은 인터페이스의 상속으로 구현된다.

* Class 상속을 통한 다형성
  - Class 상속을 통하여 다형성을 구현할 수 있다.
  - 예시 1) 동물 중에는 육식동물이 있고, 초식동물이 있다.

  ```
    class Animal {
      public void eat() {
        // 동물은 자체로 영양소를를 생성하지 못하고 외부의 음식에서 영양소를 뽑아내는 특징이 있다. 그러므로 먹는다.
        System.out.println("영양소를 생성.");
      }
    }

    class Predator extends Animal {
      @Override
      public void eat() {
          // 육식동물은 고기를 먹어서 영향소를 보충한다.
          System.out.println("고기를 먹는다.");
          super.eat();
      }

      public void hunting() {
        System.out.println("사냥한다");
      }
    }

    class HerbivorousAnimal extends Animal {
        @Override
        public void eat() {
            // 초식동물은 풀, 야채, 과일 등을 먹으면서 영양소를 보충한다.
            System.out.println("풀 뜯어 먹는다.");
            super.eat();
        }
    }

    public class Polymophism {
      
      public static void main(String[] args) throws Exception {
        // 초식동물인 소든 육식동물인 호랑이든 전부 동물이기에 동물 타입으로 인스턴스를 생성했다.
        Animal cow = new HerbivorousAnimal();
        Animal tiger = new Predator();

        // 선언된 타입은 동물이고 두 동물이 먹는 동작을 호출했다.
        System.out.println("소가 먹는다");
        cow.eat();
        System.out.println("-----------");
        System.out.println("호랑이가 먹는다");
        tiger.eat();

        // 하지만 일반적인 동물의 타입으로 선언했기 때문에
        // tiger.hunting(); [Error] 육식동물인 호랑이는 사냥을 할 수 있지만, 일반 동물의 타입으로 선언되었을 때는 사냥의 특징을 나타낼 수가 없어서 사용할 수 없다.
      }
    }

    결과:
    소가 먹는다
    풀 뜯어 먹는다.
    영양소를 생성.
    -----------
    호랑이가 먹는다
    고기를 먹는다.
    영양소를 생성.
  ```

* Interface를 통한 다형성
  - 인터페이스를 구현을 통하여 특징별로 다형성을 이룰 수 있다.
  - 예시 1) 동물은 먹을 수 있다. 그 중 포유류는 수유가 가능하고, 양서류는 수영이 가능하다. 다만, 포유류 중에 수영이 가능한 해양포유류가 있다.

  ```
    interface Iedible {
        void eat();
    }

    interface ILactating {
        void lactating();
    }

    interface Iswimmable {
        void swimming();
    }

    class Mammalia implements Iedible, ILactating {

        public void eat() {
            // 포유류는 동물이기에 먹어서 영양소를 보충한다.
            System.out.println("포유류가 먹는다.");
        }

        public void lactating() {
            // 포유류의 가장 큰 특징은 수유가 가능하다는 점이다.
            System.out.println("수유를 하여 자식에게 먹인다.");
        }
    }

    class MarineMammals extends Mammalia implements Iswimmable {
      public void swimming() {
          // 해양 포유류는 포유류지만 수영이 가능하다.
          System.out.println("해양 포유류 수영한다.");
      }
    }

    class Amphibia implements Iedible, Iswimmable {
        public void eat() {
            // 양서류도 먹는다.
            System.out.println("양서류가 먹는다.");
        }

        public void swimming() {
            // 양서류는 수영이 가능하다.
            System.out.println("수영 한다");
        }
    }

    public class Polymophism {
      
      public static void main(String[] args) throws Exception {
        Iedible cow = new Mammalia();
        Iedible frog = new Amphibia();

        Iswimmable frog2 = new Amphibia();
        Iswimmable otariidae = new MarineMammals();

        // 소가 먹는다.
        cow.eat();
        // 개구리가 먹는다.
        frog.eat();

        System.out.println("---------------------");

        // 개구리가 수영한다.
        frog2.swimming();
        // 물개가 수영한다.
        otariidae.swimming();
      }
    }

    결과:
    포유류가 먹는다.
    양서류가 먹는다.
    ---------------------
    양서류 수영 한다
    해양 포유류 수영한다.
  ```

* 다형성은 어디에 왜 사용되는가?
  - 여러 형태(타입)의 객체들을 한가지의 형태로 사용하여 관리할 수 있다.
  <!-- - 상속 및 인터페이스 구현을 통하여 확장성이 용이하고, 이를 통한 관리를 하며, 결합도를 낮출 수 있다. -->

  - 예제 1) 나는 먹이를 주고 동물들은 먹이를 먹는다. 라는 기능을 작성해보자.
    + 아래의 상황에서 육식동물에 대해 직접 먹이를 주고, 초식동물에 대해 직접 먹이를 준다면, 먹이를 주는 행위 Feed에 대하여 두 가지 타입의 메소드가 만들어 질 것이다.
    + 이런 같이 여러개의 타입을 하나의 동일한 분류의 타입으로 정의하여 공통된 하나의 기능으로 동작할 수 있는 장점이 있다.
    
  ```
    위의 예제 중 Animal 클래스와 predator, HerbivorousAnimal 클래스를 사용한다.

    public class Polymophism {

      static string feed(Animal ani) {
        // 나는 먹이를 주고,
        System.out.println("먹이를 주다.")
        // 대상이 되는 동물 ani는 먹이를 먹는다.
        return ani.eat();
      }
      
      public static void main(String[] args) throws Exception {
        Animal cow = new HerbivorousAnimal();
        Animal cat = new Predator();

        feed(cow);
        System.out.println("---------------------");
        feed(cat);
      }
    }

    결과:
    먹이를 주다.
    풀 뜯어 먹는다.
    영양소를 생성.
    ---------------------
    먹이를 주다.
    고기를 먹는다.
    영양소를 생성.
  ```

[참조] [생활코딩 - JAVA 다형성 강의 1편](https://youtu.be/WijVClKt5Z8)