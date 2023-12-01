# Spring Framework Documentation

## Table of Contents
- [1. What is IoC Container Principle?](#1-what-is-ioc-container-principle)
- [2. BeanFactory vs ApplicationContext](#2-beanfactory-vs-applicationcontext)
- [3. What is a Bean?](#3-what-is-a-bean)

## 1) What is IoC Container Principle?

**Inversion of Control (IoC)**, also known as **dependency injection (DI)**, is a process whereby objects define their dependencies (i.e., the other objects they work with) only through constructor arguments, arguments to a factory method, or properties set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean. This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes or a mechanism such as the Service Locator pattern.

### The org.springframework Packages

The `org.springframework.beans` and `org.springframework.context` packages are the basis for Spring Framework’s IoC container. The `BeanFactory` interface provides an advanced configuration mechanism capable of managing any type of object. `ApplicationContext` is a sub-interface of `BeanFactory`. It adds:

- Easier integration with Spring’s AOP features
- Message resource handling (for use in internationalization)
- Event publication
- Application-layer specific contexts such as the `WebApplicationContext` for use in web applications.

## 2) BeanFactory vs ApplicationContext

In short, the `BeanFactory` provides the configuration framework and basic functionality, while the `ApplicationContext` adds more enterprise-specific functionality. The `ApplicationContext` is a complete superset of the `BeanFactory` and is used exclusively in this chapter in descriptions of Spring’s IoC container. For more information on using the `BeanFactory` instead of the `ApplicationContext`, see the section covering the BeanFactory API.

## 3) What is a Bean?

In Spring, the objects that form the backbone of your application and are managed by the Spring IoC container are called **beans**. A bean is an object that is instantiated, assembled, and managed by a Spring IoC container. Otherwise, a bean is simply one of many objects in your application. Beans, and the dependencies among them, are reflected in the configuration metadata used by a container.
