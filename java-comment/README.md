# 자바 주석 가이드 - Javadoc

Java에서 주석을 다는 것은 코드의 가독성과 유지보수성을 높이는 데 매우 중요합니다. Javadoc은 이러한 주석을 생성하고, API 문서를 자동으로 생성하는 데 사용됩니다. 아래는 Javadoc 주석을 사용하는 방법과 권장 가이드입니다.

### 1. Javadoc 주석 기본 형식

Javadoc 주석은 `/** ... */` 사이에 작성됩니다. 기본적인 Javadoc 주석의 형식은 다음과 같습니다:

```java
/**
 * 간단한 설명
 * <p>추가 설명</p>
 * @param parameterName 매개변수 설명
 * @return 반환 값 설명
 * @throws Exception 예외 설명
 */
```

### 2. 클래스 주석

클래스의 용도와 기능을 설명합니다.

```java
/**
 * 사용자 정보를 관리하는 클래스.
 * <p>이 클래스는 사용자 정보를 저장하고, 조회하고, 수정하는 메서드를 제공합니다.</p>
 */
public class User {
    private String name;
    private int age;

    // Constructors, getters, and setters
}
```

### 3. 메서드 주석

메서드의 기능, 매개변수, 반환 값, 예외에 대해 설명합니다.

```java
/**
 * 주어진 ID로 사용자를 조회합니다.
 * 
 * @param id 조회할 사용자의 ID
 * @return 사용자 정보
 * @throws UserNotFoundException 사용자를 찾을 수 없는 경우 발생
 */
public User getUserById(Long id) throws UserNotFoundException {
    // Method implementation
}
```

### 4. 필드 주석

필드의 용도를 설명합니다.

```java
/**
 * 사용자의 이름을 저장하는 변수.
 */
private String name;
```

### 5. 생성자 주석

생성자의 용도와 매개변수에 대해 설명합니다.

```java
/**
 * 주어진 이름과 나이로 사용자를 생성합니다.
 * 
 * @param name 사용자 이름
 * @param age 사용자 나이
 */
public User(String name, int age) {
    this.name = name;
    this.age = age;
}
```

### 6. 예제

#### 클래스 주석 예제

```java
/**
 * 은행 계좌를 나타내는 클래스.
 * <p>이 클래스는 계좌 소유자의 이름, 잔액 및 관련 메서드를 포함합니다.</p>
 */
public class BankAccount {
    private String owner;
    private double balance;

    /**
     * 주어진 소유자 이름과 초기 잔액으로 은행 계좌를 생성합니다.
     * 
     * @param owner 계좌 소유자의 이름
     * @param balance 초기 잔액
     */
    public BankAccount(String owner, double balance) {
        this.owner = owner;
        this.balance = balance;
    }

    /**
     * 계좌에 금액을 입금합니다.
     * 
     * @param amount 입금할 금액
     */
    public void deposit(double amount) {
        balance += amount;
    }

    /**
     * 계좌에서 금액을 출금합니다.
     * 
     * @param amount 출금할 금액
     * @throws InsufficientFundsException 잔액이 부족할 경우 발생
     */
    public void withdraw(double amount) throws InsufficientFundsException {
        if (balance < amount) {
            throw new InsufficientFundsException("잔액이 부족합니다.");
        }
        balance -= amount;
    }

    /**
     * 현재 잔액을 반환합니다.
     * 
     * @return 현재 잔액
     */
    public double getBalance() {
        return balance;
    }
}
```

### 참고 자료

1. [Oracle Javadoc Guide](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html)
2. [How to Write Doc Comments for the Javadoc Tool](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html)
3. [Baeldung - Javadoc Tutorial](https://www.baeldung.com/javadoc)
4. [Java Code Conventions - Comments](https://www.oracle.com/java/technologies/javase/codeconventions-comments.html)
