# 객체 지향 5가지 원칙

SOLID 원칙은 객체 지향 설계의 다섯 가지 기본 원칙을 나타냅니다. Java 예제와 함께 각각의 원칙을 설명하겠습니다.

### 1. 단일 책임 원칙 (Single Responsibility Principle, SRP)

**설명**: 클래스는 하나의 책임만 가져야 하며, 클래스가 변경되는 이유는 오직 하나여야 합니다.

**Java 예시**:
```java
// 위반된 예시
public class User {
    private String username;
    private String password;

    public void setUsername(String username) {
        this.username = username;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    // 책임 1: 사용자 데이터 저장
    public void saveToDatabase() {
        // 데이터베이스 저장 로직
    }

    // 책임 2: 이메일 보내기
    public void sendEmail(String message) {
        // 이메일 전송 로직
    }
}

// 준수된 예시
public class User {
    private String username;
    private String password;

    public void setUsername(String username) {
        this.username = username;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}

public class UserRepository {
    public void saveToDatabase(User user) {
        // 데이터베이스 저장 로직
    }
}

public class EmailService {
    public void sendEmail(String message) {
        // 이메일 전송 로직
    }
}
```

### 2. 개방-폐쇄 원칙 (Open-Closed Principle, OCP)

**설명**: 소프트웨어 개체는 확장에는 열려 있어야 하지만, 수정에는 닫혀 있어야 합니다.

**Java 예시**:
```java
// 위반된 예시
public class Rectangle {
    private int width;
    private int height;

    // getter와 setter 생략

    public int calculateArea() {
        return width * height;
    }
}

public class Circle {
    private int radius;

    // getter와 setter 생략

    public int calculateArea() {
        return (int) (Math.PI * radius * radius);
    }
}

// 준수된 예시
public interface Shape {
    int calculateArea();
}

public class Rectangle implements Shape {
    private int width;
    private int height;

    // getter와 setter 생략

    @Override
    public int calculateArea() {
        return width * height;
    }
}

public class Circle implements Shape {
    private int radius;

    // getter와 setter 생략

    @Override
    public int calculateArea() {
        return (int) (Math.PI * radius * radius);
    }
}
```

### 3. 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)

**설명**: 서브타입은 그것의 기반 타입으로 치환 가능해야 합니다.

**Java 예시**:
```java
// 위반된 예시
public class Bird {
    public void fly() {
        System.out.println("Flying...");
    }
}

public class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostriches can't fly");
    }
}

// 준수된 예시
public interface Bird {
    void eat();
}

public interface FlyingBird extends Bird {
    void fly();
}

public class Sparrow implements FlyingBird {
    @Override
    public void eat() {
        System.out.println("Eating...");
    }

    @Override
    public void fly() {
        System.out.println("Flying...");
    }
}

public class Ostrich implements Bird {
    @Override
    public void eat() {
        System.out.println("Eating...");
    }
}
```

### 4. 인터페이스 분리 원칙 (Interface Segregation Principle, ISP)

**설명**: 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫습니다.

**Java 예시**:
```java
// 위반된 예시
public interface Worker {
    void work();
    void eat();
}

public class HumanWorker implements Worker {
    @Override
    public void work() {
        System.out.println("Working...");
    }

    @Override
    public void eat() {
        System.out.println("Eating...");
    }
}

public class RobotWorker implements Worker {
    @Override
    public void work() {
        System.out.println("Working...");
    }

    @Override
    public void eat() {
        throw new UnsupportedOperationException("Robots don't eat");
    }
}

// 준수된 예시
public interface Workable {
    void work();
}

public interface Eatable {
    void eat();
}

public class HumanWorker implements Workable, Eatable {
    @Override
    public void work() {
        System.out.println("Working...");
    }

    @Override
    public void eat() {
        System.out.println("Eating...");
    }
}

public class RobotWorker implements Workable {
    @Override
    public void work() {
        System.out.println("Working...");
    }
}
```

### 5. 의존 역전 원칙 (Dependency Inversion Principle, DIP)

**설명**: 고수준 모듈은 저수준 모듈에 의존해서는 안 되며, 둘 다 추상화에 의존해야 합니다.

**Java 예시**:
```java
// 위반된 예시
public class LightBulb {
    public void turnOn() {
        System.out.println("LightBulb on");
    }

    public void turnOff() {
        System.out.println("LightBulb off");
    }
}

public class Switch {
    private LightBulb lightBulb;

    public Switch(LightBulb lightBulb) {
        this.lightBulb = lightBulb;
    }

    public void operate() {
        lightBulb.turnOn();
    }
}

// 준수된 예시
public interface Switchable {
    void turnOn();
    void turnOff();
}

public class LightBulb implements Switchable {
    @Override
    public void turnOn() {
        System.out.println("LightBulb on");
    }

    @Override
    public void turnOff() {
        System.out.println("LightBulb off");
    }
}

public class Switch {
    private Switchable device;

    public Switch(Switchable device) {
        this.device = device;
    }

    public void operate() {
        device.turnOn();
    }
}
```

### 참고 자료

- [Baeldung - SOLID Principles](https://www.baeldung.com/solid-principles)
- [Wikipedia - SOLID (object-oriented design)](https://en.wikipedia.org/wiki/SOLID)