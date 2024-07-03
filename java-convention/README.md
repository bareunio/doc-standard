# 자바 컨벤션(스타일) 표준

Java 코딩 컨벤션은 코드의 가독성을 높이고 유지보수성을 향상시키기 위한 일련의 규칙과 지침을 제공합니다. 이러한 규칙은 코드가 일관되게 작성되도록 하여 여러 개발자들이 협업할 때 발생할 수 있는 문제를 줄여줍니다. 주요 자바 코딩 컨벤션 규칙은 다음과 같습니다:

### 1. **네이밍 규칙 (Naming Conventions)**

#### 클래스 이름
- 클래스 이름은 대문자로 시작하고, CamelCase 스타일을 사용합니다.
- 예: `Customer`, `AccountService`

#### 메서드 이름
- 메서드 이름은 소문자로 시작하고, CamelCase 스타일을 사용합니다.
- 예: `calculateTotal`, `getUserName`

#### 변수 이름
- 변수 이름은 소문자로 시작하고, CamelCase 스타일을 사용합니다.
- 예: `totalAmount`, `userName`

#### 상수 이름
- 상수는 모두 대문자로 작성하고, 단어는 밑줄로 구분합니다.
- 예: `MAX_USERS`, `DEFAULT_TIMEOUT`

### 2. **코드 레이아웃 (Code Layout)**

#### 들여쓰기
- 들여쓰기는 공백 4칸을 사용합니다. 탭을 사용하지 않습니다.
- 예:
  ```java
  public class Example {
      public void sampleMethod() {
          // Code block
      }
  }
  ```

#### 중괄호
- 중괄호는 새로운 줄에서 시작하지 않고, 동일한 줄에서 시작합니다.
- 예:
  ```java
  if (condition) {
      // Code block
  } else {
      // Code block
  }
  ```

### 3. **주석 (Comments)**

#### Javadoc 주석
- 모든 공개(public) 클래스와 메서드는 Javadoc 주석을 포함해야 합니다.
- 예:
  ```java
  /**
   * 이 메서드는 두 수를 더합니다.
   * @param a 첫 번째 수
   * @param b 두 번째 수
   * @return 두 수의 합
   */
  public int add(int a, int b) {
      return a + b;
  }
  ```

#### 라인 주석
- 복잡한 코드 블록 앞에 단일 줄 주석을 사용하여 코드의 목적을 설명합니다.
- 예:
  ```java
  // 사용자 이름을 가져옵니다.
  String userName = getUserName();
  ```

### 4. **코딩 스타일 (Coding Style)**

#### 중복 코드 제거
- 동일한 코드를 반복해서 사용하지 말고, 메서드로 추출하여 재사용합니다.
- 예:
  ```java
  public void process() {
      doCommonTask();
      // Other tasks
  }

  private void doCommonTask() {
      // Common code block
  }
  ```

#### 적절한 메서드 길이
- 메서드는 단일 작업만 수행하고, 너무 길지 않도록 합니다. 일반적으로 20~50줄을 넘지 않도록 합니다.

### 참고 자료
- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
- [Oracle Java Code Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-introduction.html)
- [Effective Java by Joshua Bloch](https://www.amazon.com/Effective-Java-Joshua-Bloch/dp/0134685997)
- [캠퍼스 핵데이 Java 코딩 컨벤션](https://naver.github.io/hackday-conventions-java/)
