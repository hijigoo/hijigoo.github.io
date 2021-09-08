---
layout: post
title: Abstract Factory Pattern (추상 팩토리 패턴)
category: Design Pattern
tag: [디자인 패턴, Creational]
---

## Factory
### Interface
```java
public interface PizzaIngredientFactory {
  public Dough createDough();
  public Sauce createSauce();
  public Sheese createCheese();
  public Veggies[] createVeggies();
  public Pepperoni createPepperoni();
  public Clams createClam();
}
```

### Concrete 
```java
public class NYPizzaIngredientFactory implements PizzaIngredientFactory{
  public Dough createDough() {
    return new ThinCrustDough();
  }
  public Sauce createSauce() {
    return new MarinaraSauce();
  }
  public Sheese createCheese() {
    return new ReggianoCheese();
  }
  public Veggies[] createVeggies() {
    Veggies veggies[] = {new Garlic(), new Onion(), new Mushroom(), new Redpepper()};
    return veggies;
  }
  public Pepperoni createPepperoni() {
    return new SlicedPepperoni();
  }
  public Clams createClam() {
    return new FreshClams();
  }
}
```

***

## Product
### Abstract Object
```java
public abstract class Pizza {
  String name;
  Dough dough;
  Sauce sauce;
  Veggies veggies[];
  Cheese cheese;

  abstract public void prepare();
  public void bake() {
    System.out.println("Bake for 25 minute at 350");
  }
  public void cut() {
    System.out.println("Cutting the pizza into diagonal slices");
  }
  public void box() {
    System.out.println("Place pizza in official PizzaStore box");
  }
  public void setName(String name) {
    this.name = name;
  }
  public String getName() {
    return name;
  }
  public String toString() {
    return this.getName();
  }
}
```

### Concrete Object
```java
public class CheesePizza extends Pizza {
  PizzaIngredientFactory ingredientFactory;
  public CheesePizza(PizzaIngredientFactory ingredientFactory) {
    this.ingredientFactory = ingredientFactory;
  }

  void prepare() {
    System.out.println("Preparing " + name);
    dough = ingredientFactory.createDough();
    sauce = ingredientFactory.createSauce();
    cheese = ingredientFactory.createCheese();
  }
}
```

***

## Client
```java
public class NYPizzaStore extends PizzaStore {
  protected Pizza cretePizza(String item) {
    Pizza pizza = null;
    PizzaIngredientFactory ingredientFactory = new NYPizzaIngredientFactory();
    if (item.equals("cheese")) {
      pizza = new CheesePizza(ingredientFactory);
    } else if (item.equals("veggie")) {
      pizza = new VeggiePizza(ingredientFactory);
    } else if (item.equals("clam")) {
      pizza = new ClamPizza(ingredientFactory);
    } else if (item.equals("pepperoni")) {
      pizza = new PepperoniPizza(ingredientFactory);
    }
    return pizza;
  }
}
```