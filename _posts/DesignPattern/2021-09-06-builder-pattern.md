---
layout: post
title: Builder Pattern (빌더 패턴)
category: Design Pattern
tag: [디자인 패턴, Creational]
---

## Director
```java
public class AerospaceEnginner {
  private AirplaneBuilder airplaneBuilder;

  public void setAirplaneBuilder(AirplaneBuilder ab) {
    airplaneBuilder = ab;
  }

  public Airplane getAirplane() {
    return aireplaneBuilder.getAirplane();
  }

  public void constructAirplane() {
    aireplaneBuilder.createNewAirplane();
    aireplaneBuilder.buildWings();
    aireplaneBuilder.buildPowerplant();
    aireplaneBuilder.buildAvionics();
    aireplaneBuilder.buildSeat();
  }
}
```

***

## Product
```java
public class Airplane {
  private String type;
  private float wingspan;
  private String powerplant;
  private int crewSeats;
  private int passengerSeats;
  private String avionics;
  private String customer;

  Airplane (String customer, String type) {
    this.customer = customer;
    this.type = type;
  }

  public void setWingspan(float w) { this.wingspan = w; }
  public void setPowerPlant(String p) { this.powerplant = p; }
  public void setAvionics(String a) { this.avionics = a; }
  public void setNumberSeats(int crewSeats, int passengerSeats) {
    this.crewSeats = crewSeats;
    this.passengerSeats = passengerSeats;
  }
  public String getCustomer() { return customer; }
  public String getType() { return type; }
}
```

***

## Builder 
### Abstract Builder
```java
public abstract class AirplaneBuilder {
  protected Aireplane aireplane;
  protected String customer;
  protected String type;

  public Airplane getAirplane() {
    return airplane;
  }
  public Airplane createNewAirplane() {
    airplane = new Airplane(custmer, type);
  }
  public abstract void buildWings();
  public abstract void buildPowerplant();
  public abstract void buildAvionics();
  public abstract void buildSeats();
}
```

### Concrete Builder
```java
public class CropDuster extends AirplaneBuilder {
  CropDuster (String customer) {
    super.customer = customer;
    super.type = "Crop Duster v3.4";
  }

  public void buildWings() {
    airplane.setWingspan(9f);
  }

  public void buildPowerplant() {
    airplane.setPowerplan("single piston");
  }

  public void buildAvionics() {};

  public void buildSeats() {
    airplane.setNumberSeats(1,1);
  }
}
```

```java
public class FrighterJet extends AirplaneBuilder {
  FrighterJet (String customer) {
    super.customer = customer;
    super.type = "F-35 Lighting II";
  }

  public void buildWings() {
    airplane.setWingspan(35.0f);
  }

  public void buildPowerplant() {
    airplane.setPowerplan("dual thrust vectoring");
  }

  public void buildAvionics() {
    airplane.setAvionics("military");
  };

  public void buildSeats() {
    airplane.setNumberSeats(1,0);
  }
}
```

```java
public class Glider extends AirplaneBuilder {
  Glider (String customer) {
    super.customer = customer;
    super.type = "Glider v9.0";
  }

  public void buildWings() {
    airplane.setWingspan(57.1f);
  }

  public void buildPowerplant() { }

  public void buildAvionics() { };

  public void buildSeats() {
    airplane.setNumberSeats(1,0);
  }
}
```

***

## Client
```java
public class BuilderExample {
  public static void main(String[] args) {
    // instantiate the director (hire the engineer)
    AerospaceEngineer aero = new AerospaceEngineer();

    // instantiate each concrete builder (take orders)
    AirplaneBuilder crop = new CropDuster("Farmer Joe");
    AirplaneBuilder fighter = new FighterJet("The Navy");
    AirplaneBuilder glider = new Glider("Tim Rice");

    // build a CropDuster
    aero.setAirplaneBuilder(crop);
    aero.constructAirplane();
    Airplane completedCropDuster = aero.getAirplane();
    System.out.println(completedCropDuster.getType() +
      "is completed and ready for delivery to " + 
      completedCropDuster.getCustomer()
    );
  }
}
```
