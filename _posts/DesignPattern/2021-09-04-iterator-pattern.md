---
layout: post
title: Iterator Pattern (반복자 패턴)
category: Design Pattern
tag: [디자인 패턴, Behavioral]
---

## Iterator
### Iterator Interface
```java
public interface Iterator {
  boolean hasNext();
  Object next();
}
```

### Concrete Iterator
```java
public class DinerMenuIterator implements Iterator {
  MenuItem[] items;
  int position = 0;
  
  public DinnerMenuIterator(MenuItem[] items) {
    this.items = items;
  }
  
  public Object next() {
    MenuItem menuItem = items[position];
    position++;
    return menuItem;
  }

  public boolean hasNext() {
    if (position >= items.length) return false;
    else return true;
  }
}
```

***

## Aggregate
### Aggregate Interface
```java
public interface Menu {
  public Iterator createIterator();
}
```

### Concrete Aggregate
```java
public class DinnerMenu implements Menu {
  MenuItem[] menuItems;

  // constructor
  // addItem

  public Iterator createIterator() {
    return new DinnerMenuIterator(menuItems);
  }
}
```

***

## Client

```java
public class Waitress {
  // DinnerMenu 와 유사하나 ArrayList 로 구현되어 있음
  Menu pancakeHouseMenu;
  Menu dinnerMenu;

  public waitress(Menu pancakeHouseMenu, Menu dinnerMenu) {
    this.pancakeHouseMenu = pancakeHouseMenu;
    this.dinnerMenu = dinnerMenu;
  }

  public void printMenu() {
    // 내부는 다른 Collection으로 되어 있으나, 하나의 Iterator Interface로 통일
    Iterator pancakeIterator = pancakeHouseMenu.createIterator();
    Iterator dinnerIterator = dinnerMenu.createIterator();
    
    System.out.println("menu\n---\nBREAKFAST");
    printMenu(pancakeIterator);

    System.out.println("\nLUNCH");
    printMenu(dinnerIterator);
  }

  private void printMenu(Iterator iterator) {
    while(iterator.hasNext()) {
      MenuItem menuItem = (MenuItem) iterator.next();
      System.out.println(menuItem.getName() + ", ");
    }
  }
}
```