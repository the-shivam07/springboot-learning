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
