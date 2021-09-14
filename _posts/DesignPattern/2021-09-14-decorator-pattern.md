---
layout: post
title: Decorator Pattern (데코레이터 패턴)
category: Design Pattern
tag: [디자인 패턴, Structural]
---

## Component
### Abstract Component
```java
public abstract class Beverage {
  protected String description = "Unknown Beverage"

  public String getDescription() {
    return description;
  }

  public abstract double cost();
}
```

### Concrete Component
```java
public class Espresso extends Beverage {

  public Espresso() {
    description = "Espresso"
  }

  public double cost() {
    return 1.99;
  }
}
```

***

## Decorator
### Abstract Decorator
```java
public abstract class CondimentDecorator extends Beverage {
  protected Beverage beverage;
  public abstract String getDescription();
}
```

### Concrete Decorator
```java
public class Mocha extends CondimentDecorator {

  public Mocha(Beverage beverage) {
    this.beverage = beverage // 내가 꾸미는 음료
  }

  public String getDescription() {
    return beverage.getDescription() + ", Mocha";
  }
  public double cost() {
    return .20 + beverage.cost();
  }
}
```

***

## Client
```java
public class StarbuzzCoffee {
  public static void main(String args[]) {
    // 꾸미기 X
    Beverage beverage = new Espresso();
    System.out.println(beverage.getDescription() + " $" + beverage.cost());

    // 꾸미기 O
    Beverage beverage2 = new DarkRoast();
    beverage2 = new Mocha(beverage2);
    beverage2 = new Mocha(beverage2);
    beverage2 = new Whip(beverage2);
    System.out.println(beverage2.getDescription() + " $" + beverage2.cost());

    // 꾸미기 O
    Beverage beverage3 = new DarkRoast();
    beverage3 = new Soy(beverage3);
    beverage3 = new Mocha(beverage3);
    beverage3 = new Whip(beverage3);
    System.out.println(beverage3.getDescription() + " $" + beverage3.cost());
  }
}
```