---
title: SOLID, 객체 지향 설계의 5가지 원칙
date: 2024-08-05 20 :00 :00 +09 :00
categories: [소프트웨어 공학]
tags: [se, cs, solid, srp, ocp, lsp, isp, dip ]     # TAG names should always be lowercase
---


## SOLID 원칙 : 객체 지향 설계의 기본이자 핵심

소프트웨어 개발에서 코드의 품질과 유지보수는 매우 중요한 요소입니다. 특히, 객체 지향 프로그래밍에서는 코드의 구조가 복잡해지기 쉬운데, 이때 SOLID 원칙이 큰 도움이 됩니다. SOLID는 객체 지향 설계에서 지켜야 할 다섯 가지 기본 원칙의 집합으로, 코드의 확장성, 유지보수성, 그리고 이해도를 높이기 위해 설계되었습니다.

### 왜 SOLID 원칙을 알아야 할까?

- 확장성 : SOLID 원칙은 소프트웨어를 변경하거나 확장할 때 불필요한 영향을 최소화하여, 새로운 요구 사항에 쉽게 대응할 수 있도록 합니다.
- 유지보수성 : 원칙을 지키면 코드가 명확하게 분리되어 있어, 버그 수정이나 기능 개선 시 다른 부분에 영향을 주지 않고 작업할 수 있습니다.
- 생산성 향상 : 코드가 잘 설계되어 있으면 리팩토링(코드 개선 작업)에 소요되는 시간이 줄어들어, 개발 팀의 생산성을 높일 수 있습니다.
- 코드 품질 향상 : 코드의 각 부분이 명확한 책임을 가지게 되므로, 코드의 가독성 및 재사용성이 높아집니다.


## 객체 지향이란?
객체 지향(Object-Oriented) 프로그래밍은 데이터를 '객체'라는 단위로 캡슐화하여 다루는 프로그래밍 패러다임입니다. 객체 지향의 기본 아이디어는 데이터와 그 데이터를 조작하는 메소드를 함께 묶어 클래스를 정의하고, 이 클래스를 기반으로 객체를 생성하여 문제를 해결하는 것입니다. 객체 지향의 핵심 개념은 다음과 같습니다 :

- 캡슐화 (Encapsulation) : 데이터와 메소드를 하나의 단위로 묶어 외부의 접근을 제한하고 내부 구현을 은폐합니다.
- 상속 (Inheritance) : 기존 클래스의 속성과 메소드를 새로운 클래스가 상속받아 코드 재사용성과 유지보수성을 높입니다.
- 다형성 (Polymorphism) : 동일한 인터페이스를 사용하여 다양한 객체를 처리할 수 있게 합니다.
- 추상화 (Abstraction) : 복잡한 시스템을 단순화하여 중요한 부분만 모델링합니다.

<br>

## 객체 지향 설계란?
객체 지향 설계(Object-Oriented Design, OOD)는 객체 지향 원칙을 기반으로 시스템을 설계하는 과정입니다. 이는 시스템을 객체와 클래스의 관계로 모델링하여 소프트웨어의 구조를 설계하는 방법론입니다. 객체 지향 설계는 실제 세계를 모델링하며, 다음과 같은 주요 개념을 포함합니다 :

- 클래스와 객체 : 클래스는 객체의 청사진이며, 객체는 클래스의 인스턴스입니다.
- 관계 : 클래스 간의 상속, 집합, 연관 등의 관계를 정의합니다.
- 모듈화 : 시스템을 여러 모듈로 나누어 각 모듈이 독립적으로 변경될 수 있도록 합니다.


객체 지향 설계의 특징 
- 재사용성 : 기존 클래스를 재사용하거나 상속하여 새로운 클래스를 만들 수 있습니다.
- 유지보수성 : 코드의 변경이 최소화되며, 변경의 영향이 제한적입니다.
- 유연성 : 시스템이 변화에 유연하게 대응할 수 있습니다.
- 확장성 : 새로운 기능 추가 시 기존 코드를 수정하지 않고 새로운 클래스를 추가하여 확장할 수 있습니다.

<br>
<br>

# 객체 지향 설계의 원칙

## 1. 단일 책임 원칙 (Single Responsibility Principle, SRP)
"한 클래스는 하나의 책임만 가져야 한다."
- 정의 : 클래스는 하나의 책임만 가져야 하며, 그 책임이 변경될 때만 해당 클래스를 수정해야 합니다.
- 목표 : 클래스의 책임을 명확히 하여 유지보수를 용이하게 합니다.

<br>

- 적용 방법
  - 클래스 분리 : 클래스가 여러 기능을 담당하는 경우, 각 기능에 대해 별도의 클래스를 만듭니다.
  - 기능의 응집력 : 각 클래스가 하나의 책임을 명확히 가지고 그 책임에 맞는 기능만 구현하도록 합니다.

<br>

Ex. 하나의 클래스가 청구서 생성과 발송을 모두 담당하는 경우
```
// Invoice.java
public class Invoice { // 생성과 발송 모두 담당
    private double amount; // 청구서 금액

    public Invoice(double amount) {
        this.amount = amount;
    }

    public String generateInvoice() { // 생성 담당
        return "Invoice for amount : " + amount;
    }

    public void sendInvoice(String email) { // 발송 담당
        System.out.println("Sending invoice to " + email);
    }
}
```
SRP 적용 후 코드
```
// Invoice.java
public class Invoice { // 생성 담당
    private double amount; // 청구서 금액

    public Invoice(double amount) {
        this.amount = amount;
    }

    public String generateInvoice() { // 생성 담당
        return "Invoice for amount : " + amount;
    }
}

// InvoiceSender.java
public class InvoiceSender { // 발송 담당
    public void sendInvoice(Invoice invoice, String email) { // 발송 담당
        // 청구서 내용을 이메일로 발송
        System.out.println("Sending invoice to " + email + " with content : " + invoice.generateInvoice());
    }
}
```
설명  : 청구서 생성과 발송을 담당하는 클래스를 분리합니다.

<br>

- 원칙이 적용 되었을 때 나타나는 효과
  - 유지보수성 : 각 클래스가 단일 책임만 가지므로, 하나의 책임이 변경되더라도 다른 책임에 영향을 미치지 않습니다. 이로 인해 수정이 용이합니다.
  - 확장성 : 클래스가 하나의 책임만 가지기 때문에, 새로운 기능을 추가할 때 기존의 클래스를 변경하지 않고 새로운 클래스를 추가하여 확장할 수 있습니다.
  - 명확성 : 클래스의 책임이 명확하게 정의되므로 코드가 이해하기 쉬워집니다.

<br>
<br>

## 2. 개방-폐쇄 원칙 (Open/Closed Principle, OCP)
**“소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.”**
- 정의 : 소프트웨어 요소는 확장에는 열려 있지만, 변경에는 닫혀 있어야 합니다.
- 목표 : 기존 코드를 수정하지 않고도 새로운 기능을 추가할 수 있게 합니다.

<br>

- 적용 방법
  - 추상화 활용 : 클래스를 추상화하여 고수준 모듈이 저수준 모듈의 구체적인 구현에 의존하지 않도록 합니다.
  - 인터페이스 사용 : 공통 인터페이스를 정의하고, 새로운 기능은 기존 코드를 수정하지 않고 인터페이스를 구현하여 확장합니다.

<br>

Ex. 도형의 면적을 계산하는 AreaCalculator 클래스가 도형의 종류가 추가될 때마다 수정되어야 하는 경우.
```
// AreaCalculator.java
public class AreaCalculator {
    public double calculateArea(Circle circle) { // 원의 면적 계산
        return 3.14 * circle.getRadius() * circle.getRadius();
    }

    public double calculateArea(Rectangle rectangle) { // 직사각형의 면적 계산
        return rectangle.getWidth() * rectangle.getHeight();
    }
}

// Circle.java
public class Circle {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }
}

// Rectangle.java
public class Rectangle {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    public double getWidth() {
        return width;
    }

    public double getHeight() {
        return height;
    }
}

```
OCP 적용 후 코드
```
// Shape.java
public interface Shape { // 도형 인터페이스
    double area(); // 면적 계산 메소드
}

// Circle.java
public class Circle implements Shape { // 원 클래스
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return 3.14 * radius * radius;
    }
}

// Rectangle.java
public class Rectangle implements Shape { // 직사각형 클래스
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

// AreaCalculator.java
public class AreaCalculator {
    public double calculateArea(Shape shape) { // 도형 면적 계산
        return shape.area();
    }
}
```
설명  : Shape 인터페이스를 사용하여 도형의 면적을 계산할 수 있습니다. 새로운 도형을 추가할 때 Shape 인터페이스를 구현하기만 하면 AreaCalculator 클래스를 수정할 필요가 없습니다.

<br>

- 원칙이 적용 되었을 때 나타나는 효과
  - 유지보수성 : 기존 코드를 변경하지 않고 새로운 기능을 추가할 수 있으므로, 안정성을 유지하면서도 지속적인 개선이 가능합니다.
  - 확장성 : 새로운 기능을 추가할 때 기존 클래스를 수정하지 않고도 기능을 확장할 수 있습니다.
  - 재사용성 : 기존 코드를 변경하지 않고도 다양한 기능을 조합하여 재사용할 수 있습니다.

<br>
<br>

## 3. 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)
**“프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.”**
- 정의 : 자식 클래스는 부모 클래스를 대체할 수 있어야 하며, 부모 클래스의 계약을 완전히 지켜야 합니다.
- 목표 : 자식 클래스가 부모 클래스의 기능을 완전히 대체할 수 있도록 보장합니다.

<br>

- 적용 방법
  - 계약 기반 설계 : 부모 클래스나 인터페이스에서 정의한 계약을 자식 클래스가 완전히 구현하도록 합니다.
  - 테스트 : 자식 클래스가 부모 클래스를 대체해도 프로그램의 정확성을 유지하는지 테스트합니다.

<br>

Ex. Bird 클래스에서 fly 메소드를 상속받은 Penguin 클래스가 fly 메소드를 지원하지 않는 경우.

```
// Bird.java
public abstract class Bird {
    public abstract void fly(); // 비행 메소드
}

// Sparrow.java
public class Sparrow extends Bird {
    @Override
    public void fly() {
        // 참새 비행 로직
    }
}

// Penguin.java
public class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Penguins cannot fly!");
    }
}
```
LSP 적용 후 코드
```
// Bird.java
public abstract class Bird {
    // 공통 새 속성 및 메소드
}

// FlyingBird.java
public interface FlyingBird { // 비행 가능한 새를 위한 인터페이스
    void fly();
}

// Sparrow.java
public class Sparrow extends Bird implements FlyingBird { // 비행 가능한 참새
    @Override
    public void fly() {
        // 참새 비행 로직
    }
}

// Penguin.java
public class Penguin extends Bird { // 비행 불가능한 펭귄
    // 펭귄 전용 로직
}
```
설명  : FlyingBird 인터페이스를 도입하여 비행 능력이 없는 새는 FlyingBird를 구현하지 않도록 합니다. 이렇게 하면 Penguin 클래스가 fly 메소드 때문에 오류를 발생시키지 않게 됩니다.

<br>

- 원칙이 적용 되었을 때 나타나는 효과
  - 유지보수성 : 자식 클래스가 부모 클래스를 완전히 대체할 수 있으므로, 부모 클래스를 사용하는 코드가 자식 클래스를 사용해도 문제가 없습니다.
  - 테스트 용이성 : 자식 클래스가 부모 클래스의 계약을 지키므로, 테스트 시 일관성을 유지할 수 있습니다.
  - 유연성 : 다양한 자식 클래스를 부모 클래스의 대체물로 사용하여 유연하게 시스템을 구성할 수 있습니다.

<br>
<br>

## 4. 인터페이스 분리 원칙 (Interface Segregation Principle, ISP)
**“특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.”**
- 정의 : 클라이언트는 사용하지 않는 메소드에 의존하지 말아야 합니다. 여러 개의 작은 인터페이스가 하나의 큰 인터페이스보다 낫습니다.
- 목표 : 인터페이스의 책임을 분리하여 클라이언트가 필요하지 않은 메소드에 의존하지 않도록 합니다.

<br>

- 적용 방법
  - 인터페이스 세분화 : 기능을 여러 개의 인터페이스로 나누어 각 클라이언트가 필요로 하는 인터페이스만 구현하도록 합니다.
  - 클라이언트 중심 설계 : 각 클라이언트가 필요한 메소드만 포함된 인터페이스를 제공하여, 의존성을 줄입니다.

<br>

Ex. 하나의 큰 인터페이스가 여러 기능을 제공하여, 특정 클라이언트가 사용하지 않는 메소드에 의존해야 하는 경우.

```
// Worker.java
public interface Worker {
    void work(); // 작업 수행 메소드
    void eat();  // 먹기 메소드
}

// WorkerImpl.java
public class WorkerImpl implements Worker {
    @Override
    public void work() {
        // 작업 수행 로직
    }

    @Override
    public void eat() {
        // 먹기 로직
    }
}

// Robot.java
public class Robot implements Worker {
    @Override
    public void work() {
        // 로봇 작업 수행 로직
    }

    @Override
    public void eat() {
        throw new UnsupportedOperationException("Robot cannot eat!");
    }
}
```
ISP 적용 후 코드
```
// Workable.java
public interface Workable {
    void work(); // 작업 수행 메소드
}

// Eatable.java
public interface Eatable {
    void eat(); // 먹기 메소드
}

// Worker.java
public class Worker implements Workable, Eatable {
    @Override
    public void work() {
        // 작업 수행 로직
    }

    @Override
    public void eat() {
        // 먹기 로직
    }
}

// Robot.java
public class Robot implements Workable {
    @Override
    public void work() {
        // 로봇 작업 수행 로직
    }
}
```
설명  : 각 인터페이스를 클라이언트의 필요에 따라 분리하여, 클라이언트가 필요하지 않은 메소드에 의존하지 않도록 합니다.

<br>

- 원칙이 적용 되었을 때 나타나는 효과
  - 유지보수성 : 클라이언트가 필요로 하는 메소드만 포함된 인터페이스를 사용하므로, 변경 시 영향을 최소화할 수 있습니다.
  - 유연성 : 각 클라이언트에 맞는 인터페이스를 제공함으로써, 다양한 클라이언트에 대해 유연하게 대응할 수 있습니다.
  - 명확성 : 각 인터페이스가 명확한 책임을 가지고 있으므로 코드가 이해하기 쉽습니다.

<br>
<br>

## 5. 의존성 역전 원칙 (Dependency Inversion Principle, DIP)
**"프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.”**
- 정의 : 고수준 모듈은 저수준 모듈에 의존하지 말고, 둘 다 추상화에 의존해야 합니다. 즉, 추상화된 인터페이스나 클래스에 의존하도록 합니다.
- 목표 : 구체적인 구현에 의존하지 않고 추상화된 인터페이스에 의존하여 시스템의 결합도를 낮춥니다.
<br>
- 적용 방법
  - 인터페이스 도입 : 고수준 모듈이 저수준 모듈의 구체적인 구현이 아니라 추상화된 인터페이스에 의존하도록 합니다.
  - 의존성 주입 : 추상화된 인터페이스를 사용하여 의존성을 주입하고, 구체적인 구현은 런타임에 주입하도록 합니다.

<br>

Ex. 고수준 모듈이 저수준 모듈에 직접 의존하여, 저수준 모듈의 변경이 고수준 모듈에 영향을 미치는 경우.

```
// LightBulb.java
public class LightBulb {
    public void turnOn() {
        // 조명 켜기 로직
    }

    public void turnOff() {
        // 조명 끄기 로직
    }
}

// Switch.java
public class Switch {
    private LightBulb bulb; // 저수준 모듈에 직접 의존

    public Switch(LightBulb bulb) {
        this.bulb = bulb;
    }

    public void operate() {
        bulb.turnOn(); // 조명을 켜는 작업
    }
}
```
DIP 적용 후 코드
```
// Switchable.java
public interface Switchable { // 추상화된 조작 인터페이스
    void turnOn();
    void turnOff();
}

// LightBulb.java
public class LightBulb implements Switchable { // 조명 클래스
    @Override
    public void turnOn() {
        // 조명 켜기 로직
    }

    @Override
    public void turnOff() {
        // 조명 끄기 로직
    }
}

// Switch.java
public class Switch {
    private Switchable switchable; // 추상화에 의존

    public Switch(Switchable switchable) {
        this.switchable = switchable;
    }

    public void operate() {
        switchable.turnOn(); // 조작 작업
    }
}
```

- 설명  : 
  - Switchable 인터페이스를 사용하여 고수준 모듈과 저수준 모듈 간의 의존성을 역전시킵니다.
  - Switchable 인터페이스를 도입하여 고수준 모듈 (Switch)이 저수준 모듈 (LightBulb)의 구체적인 구현에 의존하지 않도록 합니다. 이렇게 하면 시스템의 결합도를 낮추고 유연성을 높일 수 있습니다.

<br>

- 원칙이 적용 되었을 때 나타나는 효과
  - 유지보수성 : 고수준 모듈이 저수준 모듈의 구체적인 구현에 의존하지 않으므로, 저수준 모듈의 변경이 고수준 모듈에 미치는 영향을 줄일 수 있습니다.
  - 확장성 : 새로운 저수준 모듈을 추가할 때 고수준 모듈을 수정하지 않고도 교체할 수 있습니다.
  - 재사용성 : 추상화된 인터페이스를 통해 다양한 구현체를 재사용할 수 있습니다.



