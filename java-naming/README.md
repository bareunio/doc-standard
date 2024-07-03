# 자바 네이밍 가이드

## 목차 
- [클래스 네이밍 규칙](#클래스-네이밍-규칙-)
- [메서드 네이밍 규칙](#메서드-네이밍-규칙-)
- [URL 네이밍 규칙](#url-네이밍-규칙-)

## 클래스 네이밍 규칙 

Java Spring Boot 프로젝트에서 패키지 구조와 클래스 파일 네이밍 규칙을 정하는 것은 프로젝트의 유지보수성과 가독성을 높이는 데 매우 중요합니다. 다음은 패키지 구조와 결합한 클래스 파일 네이밍 규칙을 설명하는 가이드입니다.

### 1. 패키지 구조

패키지 구조는 프로젝트의 모듈화를 도와주며, 각 패키지는 특정한 기능이나 역할을 수행하는 클래스를 포함해야 합니다. 일반적으로 사용되는 패키지 구조는 다음과 같습니다:

- **`com.example.project`**: 기본 패키지
  - **`controller`**: 웹 계층을 처리하는 클래스 (REST API 엔드포인트)
  - **`service`**: 비즈니스 로직을 처리하는 클래스
  - **`repository`**: 데이터베이스와의 상호작용을 처리하는 클래스 (DAO)
  - **`model`**: 도메인 객체, 엔티티 클래스
  - **`dto`**: 데이터 전송 객체
  - **`config`**: 설정 클래스
  - **`exception`**: 예외 처리 클래스
  - **`util`**: 유틸리티 클래스

### 2. 클래스 파일 네이밍 규칙

각 클래스 파일의 이름은 그 클래스가 속한 패키지의 역할과 일치하도록 명명해야 합니다.

#### Controller 클래스

- **기능**: HTTP 요청을 처리하고, 서비스 계층을 호출하여 결과를 반환합니다.
- **네이밍**: `EntityNameController`
- **예시**: `UserController`, `ProductController`

#### Service 클래스

- **기능**: 비즈니스 로직을 처리합니다.
- **네이밍**: `EntityNameService`
- **예시**: `UserService`, `ProductService`

#### Repository 클래스

- **기능**: 데이터베이스와 상호작용을 처리합니다.
- **네이밍**: `EntityNameRepository`
- **예시**: `UserRepository`, `ProductRepository`

#### Model 클래스

- **기능**: 도메인 객체를 정의합니다.
- **네이밍**: 단순히 엔티티 이름을 사용합니다.
- **예시**: `User`, `Product`

#### DTO 클래스

- **기능**: 데이터 전송 객체로, 계층 간 데이터 전송을 담당합니다.
- **네이밍**: `EntityNameDTO`
- **예시**: `UserDTO`, `ProductDTO`

#### Config 클래스

- **기능**: 설정 관련 클래스를 정의합니다.
- **네이밍**: `SpecificConfig`
- **예시**: `DatabaseConfig`, `SecurityConfig`

#### Exception 클래스

- **기능**: 사용자 정의 예외를 정의합니다.
- **네이밍**: `SpecificException`
- **예시**: `UserNotFoundException`, `ProductNotAvailableException`

#### Util 클래스

- **기능**: 공통적으로 사용되는 유틸리티 메서드를 정의합니다.
- **네이밍**: `SpecificUtility`
- **예시**: `DateUtils`, `StringUtils`

### 예시 패키지 구조 및 클래스

```plaintext
com.example.project
├── controller
│   └── UserController.java
├── service
│   └── UserService.java
├── repository
│   └── UserRepository.java
├── model
│   └── User.java
├── dto
│   └── UserDTO.java
├── config
│   └── SecurityConfig.java
├── exception
│   └── UserNotFoundException.java
└── util
    └── DateUtils.java
```

## 메서드 네이밍 규칙 
Java Spring Boot에서 메서드 네이밍은 코드의 가독성을 높이고 유지보수를 용이하게 하기 위해 중요합니다. 메서드 네이밍은 일관성이 있어야 하며, 메서드가 수행하는 작업을 명확하게 설명해야 합니다. 다음은 Spring Boot에서 메서드 네이밍 가이드입니다:

### 기본 규칙

1. **동사로 시작**: 메서드 이름은 일반적으로 동사로 시작해야 합니다.
2. **낙타표기법(Camel Case)**: 첫 글자는 소문자로 시작하고, 이후 각 단어의 첫 글자는 대문자로 합니다.
3. **의미 전달**: 메서드 이름만으로 메서드의 기능이 무엇인지 알 수 있어야 합니다.
4. **일관성 유지**: 프로젝트 전반에 걸쳐 일관된 네이밍 규칙을 적용합니다.

### CRUD 메서드 네이밍

#### Controller 레이어

- **GET 요청**:
  - `get`, `find`를 사용합니다.
  - 예: `getUserById`, `findAllUsers`

- **POST 요청**:
  - `create`, `add`, `save`를 사용합니다.
  - 예: `createUser`, `addUser`, `saveUser`

- **PUT 요청**:
  - `update`를 사용합니다.
  - 예: `updateUser`

- **DELETE 요청**:
  - `delete`, `remove`를 사용합니다.
  - 예: `deleteUser`, `removeUser`

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public ResponseEntity<User> getUserById(@PathVariable Long id) {
        // 구현
    }

    @GetMapping
    public ResponseEntity<List<User>> findAllUsers() {
        // 구현
    }

    @PostMapping
    public ResponseEntity<User> createUser(@RequestBody User user) {
        // 구현
    }

    @PutMapping("/{id}")
    public ResponseEntity<User> updateUser(@PathVariable Long id, @RequestBody User user) {
        // 구현
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        // 구현
    }
}
```

#### Service 레이어

- **조회**:
  - `get`, `find`, `fetch`, `retrieve`를 사용합니다.
  - 예: `getUserById`, `findAllUsers`, `fetchUserDetails`

- **생성**:
  - `create`, `add`, `save`를 사용합니다.
  - 예: `createUser`, `addUser`, `saveUser`

- **수정**:
  - `update`, `modify`를 사용합니다.
  - 예: `updateUser`, `modifyUser`

- **삭제**:
  - `delete`, `remove`를 사용합니다.
  - 예: `deleteUser`, `removeUser`

```java
@Service
public class UserService {

    public User getUserById(Long id) {
        // 구현
    }

    public List<User> findAllUsers() {
        // 구현
    }

    public User createUser(User user) {
        // 구현
    }

    public User updateUser(Long id, User user) {
        // 구현
    }

    public void deleteUser(Long id) {
        // 구현
    }
}
```

#### Repository 레이어

Spring Data JPA를 사용하면 쿼리 메서드를 정의할 때도 의미 있는 이름을 사용합니다.

[참고] [JPA 쿼리 메소드](https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html)

- **조회**:
  - `findBy`, `readBy`, `queryBy`, `getBy`를 사용합니다.
  - 예: `findByUsername`, `findAll`, `findByEmail`

- **삭제**:
  - `deleteBy`, `removeBy`를 사용합니다.
  - 예: `deleteById`, `removeByUsername`

```java
public interface UserRepository extends JpaRepository<User, Long> {

    Optional<User> findByUsername(String username);

    List<User> findAll();

    void deleteById(Long id);
}
```

### MyBatis 쿼리 메서드 네이밍 (복잡한 쿼리)
MyBatis 쿼리 ID 네이밍 규칙을 정의하는 것은 프로젝트의 일관성을 유지하고 가독성을 높이는 데 중요합니다. 다음은 MyBatis 쿼리 ID를 명명할 때의 몇 가지 권장 규칙과 예시입니다.

### MyBatis 쿼리 ID 네이밍 규칙

1. **기능 기반 네이밍**:
   - 쿼리가 수행하는 작업을 나타내는 동사로 시작합니다. 예를 들어, `select`, `insert`, `update`, `delete` 등을 사용합니다.

2. **엔터티 이름 포함**:
   - 쿼리가 작동하는 엔터티의 이름을 포함합니다. 예를 들어, `User`, `Order`, `Product` 등.

3. **상세 설명 추가**:
   - 필요에 따라 쿼리의 상세 내용을 설명합니다. 예를 들어, `ById`, `ByName`, `All` 등을 사용하여 쿼리의 범위를 명확히 합니다.

4. **일관성 유지**:
   - 프로젝트 전반에 걸쳐 일관된 네이밍 규칙을 유지합니다.

5. **CamelCase 사용**:
   - ID는 CamelCase 스타일을 사용하여 단어를 구분합니다.

### 예시

#### Mapper 인터페이스

```java
public interface UserMapper {
    User selectUserById(Long id);
    List<User> selectAllUsers();
    void insertUser(User user);
    void updateUser(User user);
    void deleteUser(Long id);
}
```

#### XML 매퍼 파일

```xml
<mapper namespace="com.example.mapper.UserMapper">

    <select id="selectUserById" parameterType="Long" resultType="User">
        SELECT * FROM users WHERE id = #{id}
    </select>

    <select id="selectAllUsers" resultType="User">
        SELECT * FROM users
    </select>

    <insert id="insertUser" parameterType="User">
        INSERT INTO users (name, email, password)
        VALUES (#{name}, #{email}, #{password})
    </insert>

    <update id="updateUser" parameterType="User">
        UPDATE users
        SET name = #{name}, email = #{email}, password = #{password}
        WHERE id = #{id}
    </update>

    <delete id="deleteUser" parameterType="Long">
        DELETE FROM users WHERE id = #{id}
    </delete>

</mapper>
```

#### 네이밍 규칙 요약

1. **`select` + `엔터티 이름` + `상세 설명`**:
   - 예: `selectUserById`, `selectAllUsers`, `selectOrderDetailsByUserId`

2. **`insert` + `엔터티 이름`**:
   - 예: `insertUser`

3. **`update` + `엔터티 이름`**:
   - 예: `updateUser`

4. **`delete` + `엔터티 이름`**:
   - 예: `deleteUser`


### 기타 메서드 네이밍

- **Boolean 반환 메서드**:
  - `is`, `has`, `can`, `should`로 시작합니다.
  - 예: `isAvailable`, `hasPermission`, `canExecute`, `shouldProcess`

- **유틸리티 메서드**:
  - 동사로 시작하여 작업을 명확히 설명합니다.
  - 예: `convertToDto`, `calculateTotal`, `formatDate`

```java
public class UserUtils {

    public static boolean isValidUser(User user) {
        // 구현
    }

    public static UserDto convertToDto(User user) {
        // 구현
    }

    public static String formatDate(LocalDate date) {
        // 구현
    }
}
```

## URL 네이밍 규칙 

### API URL 네이밍 규칙
    
REST API의 요청 매핑을 위한 가이드는 RESTful 원칙을 준수하면서 이해하기 쉽고 명확한 URL 구조를 만드는 데 도움이 됩니다. 다음은 REST API의 요청 매핑을 설계할 때 고려해야 할 주요 사항과 권장 사항입니다.

1. **자원(Resource) 명명**

- **명사 사용**: 자원 이름은 명사로 작성합니다.
  - 예: `/user`, `/order`, `/product`
- **복수형 사용**: 자원 컬렉션을 나타낼 때는 복수형을 사용합니다.
  - 예: `/users`, `/orders`
- **하위 자원**: 하위 자원은 부모 자원의 ID를 포함합니다.
  - 예: `/users/{userId}/orders`, `/orders/{orderId}/items`

2. **HTTP 메서드**

- **GET**: 자원의 조회
  - 예: `GET /users`, `GET /users/{userId}`
- **POST**: 새로운 자원의 생성
  - 예: `POST /users`
- **PUT**: 기존 자원의 전체 업데이트
  - 예: `PUT /users/{userId}`
- **PATCH**: 기존 자원의 부분 업데이트
  - 예: `PATCH /users/{userId}`
- **DELETE**: 자원의 삭제
  - 예: `DELETE /users/{userId}`

3. **상태 코드**

- **200 OK**: 요청이 성공적으로 처리됨
- **201 Created**: 새로운 자원이 성공적으로 생성됨
- **204 No Content**: 요청이 성공적으로 처리되었으나 반환할 콘텐츠가 없음
- **400 Bad Request**: 잘못된 요청
- **401 Unauthorized**: 인증 실패
- **403 Forbidden**: 권한 부족
- **404 Not Found**: 자원을 찾을 수 없음
- **500 Internal Server Error**: 서버 내부 오류

4. **URL 설계**

- **리소스 컬렉션**: `GET /users`
- **리소스 단일 항목**: `GET /users/{userId}`
- **리소스 하위 컬렉션**: `GET /users/{userId}/orders`
- **리소스 필터링**: `GET /users?status=active`
- **리소스 정렬**: `GET /users?sort=name,asc`
- **리소스 페이징**: `GET /users?page=2&size=10`

#### 5. 예시

다음은 `User` 자원에 대한 REST API 요청 매핑 예시입니다.

```http
# 모든 사용자 조회
GET /users

# 사용자 생성
POST /users
{
  "name": "John Doe",
  "email": "john.doe@example.com"
}

# 특정 사용자 조회
GET /users/{userId}

# 특정 사용자 전체 업데이트
PUT /users/{userId}
{
  "name": "John Smith",
  "email": "john.smith@example.com"
}

# 특정 사용자 부분 업데이트
PATCH /users/{userId}
{
  "email": "john.newemail@example.com"
}

# 특정 사용자 삭제
DELETE /users/{userId}
```
#### 6.참고 

[RESTful API Design](https://restfulapi.net/resource-naming/)

