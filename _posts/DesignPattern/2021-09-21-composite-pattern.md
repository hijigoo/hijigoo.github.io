---
layout: post
title: Composite Pattern (컴포지트 패턴)
category: Design Pattern
tag: [디자인 패턴, Structural]
---

## Component Class
```java
public class MenuComponent {
  public void add(MenuComponent menuComponent) {
    throw new UnsupportedOperationException();
  }
  public void remove(MenuComponent menuComponent) {
    throw new UnsupportedOperationException();
  }
  public void getChild(int i) {
    throw new UnsupportedOperationException();
  }
  public Strig getName() {
    throw new UnsupportedOperationException();
  }
  public Strig getDescription() {
    throw new UnsupportedOperationException();
  }
  public double getPrice() {
    throw new UnsupportedOperationException();
  }
  public double isVegetarian() {
    throw new UnsupportedOperationException();
  }
  public double print(){
    throw new UnsupportedOperationException();
  }
}
```

***

## Leaf Class
```java
public class MenuItem extends MenuComponent {
  String name;
  String description;
  boolean vegetarian;
  double price;
  public MenuItem(String name, String description, boolean vegetarian, double price) {
    this.name = name;
    this.description = description;
    this.vegetarian = vegetarian;
    this.price = price;
  }
  public Strig getName() {
    return name;
  }
  public Strig getDescription() {
    return description;
  }
  public double getPrice() {
    return price;
  }
  public double isVegetarian() {
    return vegetarian;
  }
  public double print(){
    System.out.print(" " + getName());
    if (this.isVegetarian()) System.out.print("(v)");
    System.out.print(", " + getPrice());
    System.out.print("  --" + getDescription());
  }
}
```

***

## Composite Class
```java
public class Menu extends MenuComponent {
  ArrayList menuComponents = new ArrayList();
  String name;
  String description;
  public Menu(String name, String description) {
    this.name = name;
    this.description = description;
  }
  public void add(MenuComponent menuComponent) {
    menuComponents.add(menuComponent);
  }
  public void remove(MenuComponent menuComponent) {
    menuComponents.remove(menuComponent);
  }
  public MenuComponent getChild(int i) {
    return (MenuComponent)menuComponents.get(i);
  }
  public String getName() {return name;}
  public String getDescription() {return description;}
  public void print() {
    Iterator iterator = menuComponents.iterator();
    while (iterator.hasNext()) {
      MenuComponent menuComponent = (MenuComponent)iterator.next();
      menuComponent.print();
    }
  }
}
```

***

## Client Class
```java
public class Waitress {
  MenuComponent allMenus;
  
  public Waitress(MenuComponent allMenus) {
    this.allMenus = allMenus;
  }
  
  public void printMenu() {
    allMenus.print();
  }
}
```

***

## Using Sample
```java
public class MenuTextDrive {
  public static void main(String args[]) {
    
    // root-level menu
    MenuComponent allMenus = new Menu("ALL MENUS", "All menus combined");

    // adding mid-level Menus to root-level Menu
    MenuComponent pancakeHouseMenu = new Menu("PANCAKE HOUSE MENU", "Breakfast");
    MenuComponent dinnerMenu = new Menu("DINNER MENU", "Dinner");
    MenuComponent cafeMenu = new Menu("CAFE MENU", "Lunch");
    allMenus.add(pancakeHouseMenu);
    allMenus.add(dinnerMenu);
    allMenus.add(cafeMenu);

    // adding bottom-level Menu to mid-level Menu
    MenuComponent dessertMenu = new Menu("DESSERT MENU", "Dessert of course!");
    dinnerMenu.add(dessertMenu);

    // adding MenuItems to Menus
    pancakeHouseMenu.add(New MenuItem("K&B's Pancake Breakfast", 
      "Pancakes with scrambled eggs, and Toast", true, 2.99))
    pancakeHouseMenu.add(New MenuItem("Regular Pancake Breakfast", 
      "Pancakes with fried eggs, and saausage", false, 2.99))

    /*
    ... adding more MenuItems ...
    */

    Waitress waitress = new Waitress(allMenues);
    waitress.printMenu();
  }
}
```