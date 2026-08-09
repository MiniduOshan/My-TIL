# TIL: Java Class Concept

**Date:** August 9, 2026

Today I learned about the **class concept in Java** and how classes are used as the foundation of Object-Oriented Programming (OOP).

## What is a Class?

A **class** is a blueprint or template used to create objects.

It defines:

* **Fields** → data/state of an object
* **Methods** → behavior/actions of an object
* **Constructors** → used to initialize objects

### Basic Example

```java
public class Student {

    String name;
    int age;

    void introduce() {
        System.out.println("My name is " + name);
        System.out.println("I am " + age + " years old");
    }
}
```

Here, `Student` is a class containing fields and a method.

## Creating an Object

A class is a blueprint. We create an **object** from it using the `new` keyword.

```java
public class Main {

    public static void main(String[] args) {

        Student student1 = new Student();

        student1.name = "John";
        student1.age = 22;

        student1.introduce();
    }
}
```

### Understanding

```java
Student student1 = new Student();
```

* `Student` → class/type
* `student1` → reference variable
* `new Student()` → creates a new `Student` object

## Class vs Object

| Class              | Object               |
| ------------------ | -------------------- |
| Blueprint/template | Actual instance      |
| Defines structure  | Contains actual data |
| Example: `Student` | Example: `student1`  |

One class can be used to create multiple objects:

```java
Student student1 = new Student();
Student student2 = new Student();
```

## Key Takeaways

* A **class** is a blueprint for creating objects.
* An **object** is an instance of a class.
* Classes can contain **fields, methods, and constructors**.
* The `new` keyword is commonly used to create objects.
* Multiple objects can be created from the same class.
* Classes are a fundamental concept of **Java OOP**.
