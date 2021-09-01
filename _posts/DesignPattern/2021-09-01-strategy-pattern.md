---
layout: post
title: Strategy Pattern (전략 패턴)
category: Design Pattern
tag: [디자인 패턴, Behavioral]
---


## Context
### 1. abstract class 'Duck'
```java
public abstract class Duck {
  // object composition
  FlyBehavior flyBehavior;
  QuackBehavior quackBehavior;
  public Duck() {}

  public abstract void display();

  // inheritance
  public void swim() {
    System.out.println("All ducks float, event decoys!");
  }

  // delegation
  public void performFly() {
    flyBehavior.fly();  
  }
  public void performQuack() {
    quackBehavior.quack();
  }

  // set behavior
  public void setFlyBehavior(FlyBehavior fb) {
    flyBehavior = fb;
  }

  public void setFlyBehavior(QuackBehavior qb) {
    quackBehavior = qb;
  }
}

```

***

## Strategy

### 1. FlyBehavior
```java
public interface FlyBehavior {
  public void fly();
}

public class FlyWithWings implements FlyBehavior {
  public void fly() {
    System.out.println("I'm flying!");
  }
}

public class FlyNoWay implements FlyBehavior {
  public void fly() {
    System.out.println("I can't fly!");
  }
}

public class FlyRocketPowered implements FlyBehavior {
  public void fly() {
    System.out.println("I'm flying with a rocket!");
  }
}
```

### 2. QuackBehavior
```java
public interface QuackBehavior {
  public void fly();
}

public class Quack implements QuackBehavior {
  public void quack() {
    System.out.println("Quack");
  }
}

public class MuteQuack implements QuackBehavior {
  public void quack() {
    System.out.println("<< slience >>");
  }
}

public class Squeak implements QuackBehavior {
  public void quack() {
    System.out.println("Squeak");
  }
}
```

## Sample
### 1. MallardDuck
필요한 Strategy를 직접 생성해서 사용한다.

```java
public class MallardDuck extends Duck {
  public MallarDuck() {
    quackBehavior = new Quack();
    flyBehavior = new FlyWithWings();
  }
  public void display() {
    System.out.println("I'm a real Mallard Duck");
  }
}
```

### 2. ModelDuck
필요한 Strategy를 Dynamic 하게 설정한다.

```java
public class ModelDuck extends Duck {
  public ModelDuck() {
    quackBehavior = new Quack();
    flyBehavior = new FlyNoWay();
  }
  public void display() {
    System.out.println("I'm a model Duck");
  }
}
```
### 3. 실행
```java
public class MiniDuckSimulator {
  public static void main(String[] args) {
    Duck mallard = new MallardDuck();
    mallard.performQuack(); // Quack
    mallard.performFly(); // I'm flying!

    Duck model = new ModelDuck();
    model.performQuack(); // Quack
    model.performFly(); // I can't fly
    model.setFlyBehavior(new FlyRocketPowered());
    model.performFly(); // I'm flying with a rocket!
  }
}
```