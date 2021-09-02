---
layout: post
title: Template Method Pattern (템플릿 메소드 패턴)
category: Design Pattern
tag: [디자인 패턴, Behavioral]
---


## Abstract Class
```java
public abstract CaffeineBeverage {

  // Template Method
  final void prepareRecipe() {
    boilWater();
    brew();
    pourInCup();
    addCondiments();
  }
  abstract void brew();
  abstract void addCondiments();

  public void boilWater() {
    System.out.println("Boiling water");
  }

  public void pourInCup() {
    System.out.println("Pouring into Cup");
  }
}
```

***

## Concrete Class
```java
public class Coffee extends CaffeineBeverage {
  public void brew() {
    System.out.println("Dripping Coffee through filter");
  }
  public void addCondiments() {
    System.out.println("Adding Sugar and Milk");
  }
}
```
```java
public class Tea extends CaffeineBeverage {
  public void brew() {
    System.out.println("Steeping the tea");
  }
  public void addCondiments() {
    System.out.println("Adding Lemon");
  }
}

```
