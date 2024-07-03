# 도메인 주도 설계(DDD)

도메인 주도 설계(DDD)는 복잡한 소프트웨어 프로젝트를 구조화하는 데 유용한 방법론입니다. DDD에서는 도메인 모델을 중심으로 시스템을 설계하고, 도메인 논리를 중심으로 패키지 구조를 나눕니다. Spring Boot와 같은 프레임워크를 사용하여 DDD 원칙을 적용할 때, 패키지 구조를 적절하게 나누는 것은 중요합니다. 다음은 DDD 패키지 구조에 대한 상세 설명입니다.

### 기본 패키지 구조

DDD 패키지 구조는 도메인 모델을 중심으로 구성되며, 각 도메인별로 책임을 분리합니다. 다음은 일반적인 DDD 패키지 구조의 예시입니다:

```
com.example
├── common
│   ├── exception
│   └── util
├── config
├── domain
│   ├── (domain1)
│   │   ├── controller
│   │   ├── service
│   │   ├── dao
│   │   ├── model
│   │   ├── dto
│   │   └── exception
│   ├── (domain2)
│   │   ├── controller
│   │   ├── service
│   │   ├── dao
│   │   ├── model
│   │   ├── dto
│   │   └── exception
│   └── (domain3)
│       ├── controller
│       ├── service
│       ├── dao
│       ├── model
│       ├── dto
│       └── exception
```

### 각 패키지의 역할

#### 1. common

- **exception**: 공통 예외 클래스.
- **util**: 공통 유틸리티 클래스.

#### 2. config

- Spring Boot 설정 클래스 (예: 데이터베이스 설정, 보안 설정 등).

#### 3. domain

각 도메인은 다음과 같은 하위 패키지를 가집니다:

- **controller**: 웹 계층, HTTP 요청을 처리합니다. RESTful API 엔드포인트를 포함합니다.
- **service**: 비즈니스 로직을 처리합니다.
- **dao**: 데이터베이스와의 상호작용을 처리합니다. 주로 리포지토리 인터페이스가 포함됩니다.
- **model**: 도메인 엔티티 클래스가 포함됩니다.
- **dto**: 데이터 전송 객체. 서비스 계층과 웹 계층 간의 데이터를 전달합니다.
- **exception**: 도메인별 예외 클래스.

### 예시 패키지 구조 및 클래스

#### order 도메인 예시

```plaintext
com.example.domain.order
├── controller
│   └── OrderController.java
├── service
│   └── OrderService.java
├── dao
│   └── OrderRepository.java
├── model
│   └── Order.java
├── dto
│   └── OrderDTO.java
└── exception
    └── OrderNotFoundException.java
```

#### OrderController.java

```java
package com.example.domain.order.controller;

import com.example.domain.order.dto.OrderDTO;
import com.example.domain.order.service.OrderService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/orders")
public class OrderController {

    @Autowired
    private OrderService orderService;

    @GetMapping
    public List<OrderDTO> getAllOrders() {
        return orderService.getAllOrders();
    }

    @GetMapping("/{id}")
    public OrderDTO getOrderById(@PathVariable Long id) {
        return orderService.getOrderById(id);
    }

    @PostMapping
    public OrderDTO createOrder(@RequestBody OrderDTO orderDTO) {
        return orderService.createOrder(orderDTO);
    }

    @PutMapping("/{id}")
    public OrderDTO updateOrder(@PathVariable Long id, @RequestBody OrderDTO orderDTO) {
        return orderService.updateOrder(id, orderDTO);
    }

    @DeleteMapping("/{id}")
    public void deleteOrder(@PathVariable Long id) {
        orderService.deleteOrder(id);
    }
}
```

#### OrderService.java

```java
package com.example.domain.order.service;

import com.example.domain.order.dao.OrderRepository;
import com.example.domain.order.dto.OrderDTO;
import com.example.domain.order.model.Order;
import com.example.domain.order.exception.OrderNotFoundException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.stream.Collectors;

@Service
public class OrderService {

    @Autowired
    private OrderRepository orderRepository;

    public List<OrderDTO> getAllOrders() {
        return orderRepository.findAll().stream()
                .map(order -> new OrderDTO(order))
                .collect(Collectors.toList());
    }

    public OrderDTO getOrderById(Long id) {
        Order order = orderRepository.findById(id)
                .orElseThrow(() -> new OrderNotFoundException(id));
        return new OrderDTO(order);
    }

    public OrderDTO createOrder(OrderDTO orderDTO) {
        Order order = new Order(orderDTO);
        orderRepository.save(order);
        return new OrderDTO(order);
    }

    public OrderDTO updateOrder(Long id, OrderDTO orderDTO) {
        Order order = orderRepository.findById(id)
                .orElseThrow(() -> new OrderNotFoundException(id));
        order.update(orderDTO);
        orderRepository.save(order);
        return new OrderDTO(order);
    }

    public void deleteOrder(Long id) {
        orderRepository.deleteById(id);
    }
}
```

#### OrderRepository.java

```java
package com.example.domain.order.dao;

import com.example.domain.order.model.Order;
import org.springframework.data.jpa.repository.JpaRepository;

public interface OrderRepository extends JpaRepository<Order, Long> {
}
```
