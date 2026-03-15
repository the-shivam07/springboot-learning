# Getting Started with Spring Framework

## Overview

In this example, we build a **GameRunner application** that can run different games like **Mario, SuperContra, and Pacman**.

The goal is to understand how **Spring Framework helps reduce tight coupling and create loosely coupled applications**.

The application evolves through multiple **iterations** to improve the design.

---

# Iteration 1: Tightly Coupled Java Code

### Concept

In the first approach, the `GameRunner` class directly creates and uses a specific game class like `MarioGame`.

### Example Code

```java
public class GameRunner {

    MarioGame game = new MarioGame();

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

### Problems with Tight Coupling

* `GameRunner` is directly dependent on `MarioGame`
* Switching to another game requires modifying the code
* Not flexible and difficult to maintain

---

# Iteration 2: Loose Coupling Using Interfaces

### Concept

To remove tight dependency, we introduce an interface called **GamingConsole**.

This interface defines common methods that every game must implement.

### GamingConsole Interface

```java
public interface GamingConsole {

    void up();
    void down();
    void left();
    void right();
}
```

### MarioGame Implementation

```java
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

### GameRunner Using Interface

```java
public class GameRunner {

    GamingConsole game;

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

### Advantages

* Loose coupling
* GameRunner works with any game
* Easy to add new games

---

# Iteration 3: Loose Coupling Using Spring (Spring Level 1)

### Concept

Instead of manually creating objects, **Spring Framework manages object creation and dependency wiring**.

These objects are called **Spring Beans**.

### Example

```java
@SpringBootApplication
public class GamingApplication {

    public static void main(String[] args) {

        ApplicationContext context =
                SpringApplication.run(GamingApplication.class, args);

        GameRunner runner = context.getBean(GameRunner.class);
        runner.run();
    }
}
```

### Benefits

* Spring manages objects
* No need for manual object creation
* Better dependency management

---

# Iteration 4: Spring Level 2 (Using Annotations)

### Concept

Spring provides annotations to automatically create and inject dependencies.

### Important Spring Annotations

| Annotation               | Purpose                            |
| ------------------------ | ---------------------------------- |
| `@Component`             | Marks a class as a Spring Bean     |
| `@Autowired`             | Automatically injects dependencies |
| `@SpringBootApplication` | Main Spring Boot configuration     |

### Example

```java
@Component
public class GameRunner {

    @Autowired
    GamingConsole game;

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

### Advantages

* Automatic dependency injection
* Cleaner code
* Less configuration

---

# Key Concepts Learned

### 1. Tight Coupling

Classes are highly dependent on each other.

### 2. Loose Coupling

Classes are independent and interact using interfaces.

### 3. Interface

Defines a contract that multiple classes can implement.

### 4. Spring Beans

Objects managed by the Spring container.

### 5. Dependency Injection

Spring automatically provides required objects to classes.

---

# Summary

In this example we learned how application design evolves:

1. Tightly Coupled Java Code
2. Loose Coupling using Interfaces
3. Spring managing objects using Beans
4. Spring using annotations for automatic dependency injection

Spring helps developers build **flexible, maintainable, and scalable applications**.



# Spring Framework Basics – Coupling, Interfaces and Spring Container

## 1. Tight Coupling

Tight coupling occurs when one class directly depends on another class.
This means if we change one class, we must also change the dependent class.

### Example

If `GameRunner` directly creates `MarioGame`, it becomes tightly coupled.

```java
public class GameRunner {

    MarioGame game = new MarioGame();

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

### Problems with Tight Coupling

* Code is not flexible
* Hard to switch to another implementation
* Difficult to maintain and extend

---

# 2. Loose Coupling

Loose coupling means classes are **less dependent on each other**.

Instead of depending on a specific class, we depend on an **interface**.

This allows us to easily switch between implementations.

Example:

GameRunner can run **Mario, SuperContra, or Pacman** without changing its code.

---

# 3. Using Interfaces for Loose Coupling

To achieve loose coupling, we create an interface called `GamingConsole`.

### GamingConsole Interface

```java
package com.in28minutes.learn_spring_framework;

public interface GamingConsole {

    void up();
    void down();
    void left();
    void right();

}
```

### Example Implementation

```java
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

Now we can create other games like:

* SuperContraGame
* PacmanGame

All implement the same interface.

---

# 4. Spring Container

Spring Container is responsible for:

* Creating objects
* Managing objects
* Injecting dependencies
* Managing lifecycle of beans

In simple words:

Spring container manages **Spring Beans**.

---

# 5. Types of Spring Containers

### 1. BeanFactory

BeanFactory is the **basic Spring container**.

Features:

* Basic dependency injection
* Lightweight container
* Suitable for simple applications

---

### 2. ApplicationContext

ApplicationContext is the **advanced Spring container**.

Features:

* Enterprise features
* Easy integration with web applications
* Internationalization support
* Integration with Spring AOP

Most **enterprise applications use ApplicationContext**.

---

# 6. IOC Container (Inversion of Control)

Spring uses an **IOC Container** to manage objects.

Instead of creating objects manually:

```
new Object()
```

Spring creates and manages objects automatically.

This concept is called **Inversion of Control (IOC)**.

---

# 7. Questions in Spring (Important Concepts)

### Spring Container vs IOC Container

Both refer to the same concept where Spring manages objects.

---

### Java Bean vs Spring Bean

Java Bean:

* Simple Java class
* Contains properties and getters/setters

Spring Bean:

* Object managed by Spring Container

---

### How to list all Spring Beans?

We can use ApplicationContext to list all beans.

Example:

```java
String[] beanNames = context.getBeanDefinitionNames();
```

---

# 8. Topics Covered in This Lecture

1. Tight Coupling
2. Loose Coupling
3. Java Interfaces
4. Spring Container
5. Application Context
6. Basic Spring Annotations
7. Dependency Injection
8. Auto Wiring
9. Java Bean vs Spring Bean

---

# Summary

In this lecture we learned:

* What is Tight Coupling
* How to achieve Loose Coupling
* How Interfaces help reduce dependency
* What is Spring Container
* Difference between BeanFactory and ApplicationContext
* Basic understanding of IOC and Dependency Injection

Spring Framework helps developers create **flexible, maintainable, and loosely coupled applications**.

