# Spring Annotations and Dependency Injection

Spring Framework provides several annotations that help developers create and manage objects easily.
These annotations simplify configuration and enable **Dependency Injection**.

---

# What is a Spring Bean?

A **Spring Bean** is an object that is created and managed by the **Spring Container**.

Instead of creating objects manually using `new`, Spring creates and manages them automatically.

### Example

```java
Person person = new Person();
```

In Spring applications, the **container manages these objects automatically**.

---

# @Component Annotation

`@Component` is used to tell Spring that a class should be managed by the **Spring Container**.

When the application starts, Spring scans the project and automatically creates objects for classes marked with `@Component`.

### Example

```java
import org.springframework.stereotype.Component;

@Component
public class MarioGame implements GamingConsole {

    public void up() {
        System.out.println("Jump");
    }

    public void down() {
        System.out.println("Go into hole");
    }

    public void left() {
        System.out.println("Move backward");
    }

    public void right() {
        System.out.println("Move forward");
    }
}
```

Spring will automatically create a bean of `MarioGame`.

---

# Dependency Injection

Dependency Injection means **Spring automatically provides the required object to a class**.

Example:

`GameRunner` needs a `GamingConsole` object.

Instead of creating it manually, Spring injects the dependency automatically.

### Example

```java
import org.springframework.stereotype.Component;

@Component
public class GameRunner {

    private GamingConsole game;

    public GameRunner(GamingConsole game) {
        this.game = game;
    }

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

Spring automatically injects the correct implementation of `GamingConsole`.

---

# Types of Dependency Injection

There are mainly three types of dependency injection.

---

## 1. Constructor Injection (Recommended)

Constructor Injection is the **recommended approach in Spring**.

```java
public GameRunner(GamingConsole game) {
    this.game = game;
}
```

### Advantages

* Makes objects immutable
* Easier to test
* Recommended by Spring

---

## 2. Setter Injection

Setter Injection uses setter methods to inject dependencies.

```java
@Autowired
public void setGame(GamingConsole game) {
    this.game = game;
}
```

---

## 3. Field Injection

Field Injection directly injects dependencies into class fields.

```java
@Autowired
private GamingConsole game;
```

This approach is **not recommended for large applications**.

---

# @Configuration Annotation

`@Configuration` tells Spring that the class contains **bean definitions**.

Example:

```java
import org.springframework.context.annotation.Configuration;

@Configuration
public class GamingConfiguration {

}
```

This class can define beans using the `@Bean` annotation.

---

# @Bean Annotation

`@Bean` is used to manually create and register objects inside the **Spring Container**.

Example:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public GamingConsole game() {
        return new MarioGame();
    }
}
```

Spring will create and manage a bean of `MarioGame`.

---

# @Primary Annotation

When multiple beans of the same type exist, Spring may not know which one to use.

`@Primary` tells Spring which bean should be used by default.

### Example

```java
@Component
@Primary
public class MarioGame implements GamingConsole {

}
```

Now Spring will prefer the `MarioGame` bean.

---

# @Qualifier Annotation

If multiple beans exist and we want a **specific bean**, we use `@Qualifier`.

### Example

```java
@Component
public class GameRunner {

    private GamingConsole game;

    public GameRunner(@Qualifier("pacmanGame") GamingConsole game) {
        this.game = game;
    }
}
```

This tells Spring to inject the **PacmanGame** implementation.

---

# Summary

In this section we learned:

* What is a Spring Bean
* `@Component` annotation
* Dependency Injection
* Types of Dependency Injection
* `@Configuration` annotation
* `@Bean` annotation
* `@Primary` annotation
* `@Qualifier` annotation

These concepts are essential for building **Spring Boot applications and microservices**.
