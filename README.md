# Spring Framework Documentation

## Table of Contents
- [1. What is IoC Container Principle?](#1-what-is-ioc-container-principle)
- [2. BeanFactory vs ApplicationContext](#2-beanfactory-vs-applicationcontext)
- [3. What is a Bean?](#3-what-is-a-bean)

## 1) What is IoC Container Principle?

**Inversion of Control (IoC)**, also known as **dependency injection (DI)**, is a process whereby objects define their dependencies (i.e., the other objects they work with) only through constructor arguments, arguments to a factory method, or properties set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean. This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes or a mechanism such as the Service Locator pattern.

The `org.springframework.beans` and `org.springframework.context` packages are the basis for Spring Framework’s IoC container. The `BeanFactory` interface provides an advanced configuration mechanism capable of managing any type of object. `ApplicationContext` is a sub-interface of `BeanFactory`. It adds:

- Easier integration with Spring’s AOP features
- Message resource handling (for use in internationalization)
- Event publication
- Application-layer specific contexts such as the `WebApplicationContext` for use in web applications.

In the Spring Framework, **Inversion of Control (IoC)** is a core principle, whereas **Dependency Injection (DI)** is its practical implementation. 
Let's consider the scenario of writing and executing tests.

### Classic Control Flow in Testing

Initially, we might write tests and trigger their execution manually. This approach follows a classic control flow, where we have complete control over the test lifecycle and its execution order.

```java
public class AnyTest {
    public static void globalSetUp() { ... }
    public void setUp() { ... }
    public void anyTest1() { ... }
    public void anyTest2() { ... }
    public void tearDown() { ... }
    public static void globalTearDown() { ... }
}

public class AnyTestRunner {
    public static void main(String[] args) {
        AnyTest test = new AnyTest();
        // Manual test execution
        test.globalSetUp();
        test.setUp();
        test.anyTest1();
        test.tearDown();
        test.setUp();
        test.anyTest2();
        test.tearDown();
        test.globalTearDown();
    }
}
```

### Inverted Control Flow with Testing Frameworks
When a testing framework comes into play, it takes over the management of the test lifecycle. The testing class is still authored by us, but we now provide metadata to the framework in the form of annotations to indicate the framework what to run and in what order. It is no longer us who trigger the test methods; instead, the testing framework detects the test class, reads the metadata, and manages the test lifecycle.
```java
import org.junit.jupiter.api.*;

public class AnyTest {
    @BeforeAll
    public static void globalSetUp() { ... }

    @BeforeEach
    public void setUp() { ... }

    @Test
    public void anyTest1() { ... }

    @Test
    public void anyTest2() { ... }

    @AfterEach
    public void tearDown() { ... }

    @AfterAll
    public static void globalTearDown() { ... }
}
```
By utilizing a framework that manages the lifecycle of tests, we essentially invert the control flow. This aligns with the IoC principle, where the framework, rather than the user, takes charge of the execution process.

## 2) BeanFactory vs ApplicationContext

In short, the `BeanFactory` provides the configuration framework and basic functionality, while the `ApplicationContext` adds more enterprise-specific functionality. The `ApplicationContext` is a complete superset of the `BeanFactory` and is used exclusively in this chapter in descriptions of Spring’s IoC container. For more information on using the `BeanFactory` instead of the `ApplicationContext`, see the section covering the BeanFactory API.

## 3) What is a Bean?

In Spring, the objects that form the backbone of your application and are managed by the Spring IoC container are called **beans**. A bean is an object that is instantiated, assembled, and managed by a Spring IoC container. Otherwise, a bean is simply one of many objects in your application. Beans, and the dependencies among them, are reflected in the configuration metadata used by a container.

## 4) Какой порядок у процесса создания Бина
![Снимок экрана 2023-12-01 в 19 20 28](https://github.com/Nurs-27/2023-11-otus-spring-nursultan/assets/15341062/b4e32615-5f73-447e-9d9d-955352beb751)
Чтение метаданных: Spring сначала читает метаданные, которые определяют бины. Метаданные могут быть предоставлены в виде XML-конфигурации, аннотаций в коде или через Java-конфигурацию.

Чтение всех необходимых классов по метаданным: Контейнер анализирует метаданные и загружает соответствующие классы, которые используются для создания бинов.

Создание всех бинов: Контейнер инстанцирует бины, используя информацию, полученную из метаданных и загруженных классов.

Задание зависимостей: Зависимости между бинами вводятся с использованием внедрения зависимостей. Это может быть сделано через конструкторы, сеттеры или фабричные методы.
