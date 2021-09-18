---
layout: post
title: Adapater Pattern (아답타 패턴)
category: Design Pattern
tag: [디자인 패턴, Structural]
---

## Target
### Target interface
```java
public interface Duck {
  public void quack();
  public void fly();
}
```

### Target Sample Object
```java
public class MallarDuck implements Duck {
  public void quack() {
    System.out.println("Quack");
  }
  public void fly() {
    System.out.println("I am flying");
  }
}
```

***

## Adaptee
### Adaptee interface
```java
public interface Turkey {
  public void gobble();
  public void fly();
}
```

### Adaptee Sample Object
```java
public class WildTurkey implements Turkey {
  public void gobble() {
    System.out.println("Gobble Gobble");
  }
  public void fly() {
    System.out.println("I'm flying a short distance");
  }
}
```

***

## Turkey Adapter
```java
// implement Duck for Turkey
public class  TurkeyAdapter implements Duck {
  Turkey turkey;

  public TurkeyAdapter(Turkey turkey) {
    this.turkey = turkey;
  }

  // adapt
  public void quack() {
    turkey.google();
  }

  // adapt
  public void fly() {
    for (int i = 0; i < 5; i++) {
      turkey.fly();
    };
  }
}
```

***

## Client
```java
public class DuckTestDrive {
  public static void main(String[] args) {
    MallarDuck duck = new MallarDuck();
    
    WildTurkey turkey = new WildTurkey();
    Duck turkeyAdapyer = new TurkeyAdapter(turkey);

    System.out.println("The Turkey says...");
    turkey.gobble();
    turkey.fly();

    System.out.println("The Duck says...");
    duck.quack();
    duck.fly();

    System.out.println("The TurkeyAdapyer says...");
    turkeyAdapyer.quack();
    turkeyAdapyer.fly();
  }
}

```