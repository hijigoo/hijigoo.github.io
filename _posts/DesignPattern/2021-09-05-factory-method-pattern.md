---
layout: post
title: Factory Method Pattern (팩토리 메소드 패턴)
category: Design Pattern
tag: [디자인 패턴, Creational]
---

## Creator
### Abstract Creater 
```java
public abstract class PizzaStore {
  public Pizza orderPizza(String type) {
    Pizza pizza;
    pizza = createPizza(type);

    pizza.prepare();
    pizza.bake();
    pizza.cut();
    pizza.box();

    return pizza;
  }

  // factory method
  protected abstract Pizza createPizza(String type);
}
```

### Concrete Creater 
```java
public class NYPizzaStore extends PizzaStore{
  // factory method
  public Pizza createPizza(String type) {
    Pizza pizza;
    if (type.equals("cheese")) {
      pizza = new NYStyleCheesePizza();
    } else if (type.equals("veggie")) {
      pizza = new NYStyleVeggiePizza();
    }
    return pizza;
  }
}
```

```java
public class ChicagoPizzaStore extends PizzaStore{
  // factory method
  public Pizza createPizza(String type) {
    Pizza pizza;
    if (type.equals("cheese")) {
      pizza = new ChicagoStyleCheesePizza();
    } else if (type.equals("veggie")) {
      pizza = new ChicagoStyleVeggiePizza();
    }
    return pizza;
  }
}
```

***

## Product
### Abstract Product
```java
public abstract class Pizza {
  String name;
  String dough;
  String sauce;
  ArrayList toppings = new ArrayList();

  void prepare() {
    System.out.println("Preparing " + name);
    System.out.println("Tossing dough...");
    System.out.println("Adding sauce..");
    System.out.println("Adding toppings: ");
    for (int i = 0; i < toppings.size(); < i++) {
      System.out.println("  " + toppings.get(i));
    }
  }

  void bake() {
    System.out.println("Bake for 25 minutes at 350");
  }

  void cut() {
    System.out.println("Cutting the pizza into diagonal slices");
  }

  void box() {
    System.out.println("Place pizza in official PizzaStore box");
  }
}
```

### Concrete Product 
```java
public class NYStyleCheesePizza extends Pizza {
  public NYStyleCheesePizza() {
    name = "NY Style Sauce and Cheese Pizza";
    dough = "Thin Crust Dough";
    sauce = "Marinara Sauce";
    toppings.add("Grated Reggiano Cheese");
  }
}
```

```java
public class ChicagoStyleCheesePizza extends Pizza {
  public ChicagoStyleCheesePizza() {
    name = "Chicago Style Deep Dish and Cheese Pizza";
    dough = "Extra Thick Crust Dough";
    sauce = "Plum Tomato Sauce";
    toppings.add("Shredded Mozzarella Cheese");
  }
  void cut() {
    System.out.println("Cutting the pizza into square slices");
  }
}
```