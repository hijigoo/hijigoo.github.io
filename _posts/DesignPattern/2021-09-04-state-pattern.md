---
layout: post
title: State Pattern (상태 패턴)
category: Design Pattern
tag: [디자인 패턴, Behavioral]
---

## Context
```java
public class GumballMachine {
  State soldOutState;
  State noQuarterState;
  State hasQuarterState;
  State soldState;

  State state = soldOutState;
  int count = 0;

  public GumballMachine(int numberGumballs) {
    soldOutState = new SoldOutState(this);
    noQuarterState = new NoQuarterState(this);
    hasQuarterState = new HasQuarterState(this);
    soldState = new SoldState(this);

    this.count = numberGumballs;
    if (numberGumballs > 0) {
      state = noQuarterState;
    }
  }

  public void insertQuarter() {
    state.insertQuarter();
  }

  public void ejectQuater() {
    state.ejectQuater();
  }

  public void turnCrank() {
    state.turnCrank();
  }

  void setState(State state) {
    this.state = state;
  }

  void releaseBall() {
    System.out.println("A gumball comes rolling out the slot...");
    if (count != 0) {
      count = count - 1;
    }
  }

  // 각 State 객체를 위한 getter 및 기타 메소드
}
```

***

## State
### State Interface
```java
public interface State {
  public void insertQuater();
  public void ejectQuater();
  public void turnCrank();
  public void dispense();
}
```

### Concrete State
```java
public class NoQuarterState implements State {
  GumballMachine gumballMachine;

  public NoQuarterState(GumballMachine gumballMachine) {
    this.gumballMachine = gumballMachine;
  }

  public void insertQuater() {
    System.out.println("You inserted a quater");
    gumballMachine.setState(gumballMachine.getHasQuarterState());
  }

  public void ejectQuater() {
    System.out.println("You haven't inserted a quarter");
  }

  public void turnCrank() {
    System.out.println("You turned, but there's no quarter");
  }

  public void dispense() {
    System.out.println("No Gumball dispensed");
  }
}
```

```java
public class HasQuarterState implements State {
  GumballMachine gumballMachine;

  public HasQuarterState(GumballMachine gumballMachine) {
    this.gumballMachine = gumballMachine;
  }

  public void insertQuater() {
    System.out.println("You can't insert another quarter");
  }

  public void ejectQuater() {
    System.out.println("Quarter returned");
    gumballMachine.setState(gumballMachine.getNoQuarterState());
  }

  public void turnCrank() {
    System.out.println("You turned...");
    gumballMachine.setState(gumballMachine.getSoldState());
    gumballMachine.dispense();
  }

  public void dispense() {
    System.out.println("No Gumball dispensed");
  }
}
```

```java
public class SoldState implements State {
  GumballMachine gumballMachine;

  public SoldState(GumballMachine gumballMachine) {
    this.gumballMachine = gumballMachine;
  }

  public void insertQuater() {
    System.out.println("Please wait, we're already giving you a gumball");
    gumballMachine.setState(gumballMachine.getHasQuarterState());
  }

  public void ejectQuater() {
    System.out.println("Sorry, you already turned the crank");
  }

  public void turnCrank() {
    System.out.println("Turning twice doesn't doesn't get you another gumball!");
  }

  public void dispense() {
    gumballMachine.releaseBall();
    if (gumballMachine.getCount() > 0) {
       gumballMachine.setState(gumballMachine.getNoQuarterState());
    } else {
      System.out.println("Oops, out of gumballs!");
      gumballMachine.setState(gumballMachine.getSoldOutState());
    }
  }
}
```
