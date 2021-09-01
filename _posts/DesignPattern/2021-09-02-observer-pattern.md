---
layout: post
title: Observer Pattern (옵저버 패턴)
category: Design Pattern
tag: [디자인 패턴, Behavioral]
---


## Interfaces
### 1. Subject
```java
public interface Subject {
  public void registerObserver(Observer o);
  public void removeObserver(Observer o);
  public void notifyObservers();
}
```

### 2. Observer
```java
public interface Observer {
  public void update(float temp, float humidity, float pressure);
}
```

### 3. Display Element (Optional)
```java
public interface DisplayElement {
  public void display();
}
```

***

## Implements
### 1. Concrete Subject 
```java
public class WeatherData implements Subject {
  private ArrayList observers;
  private float temperature;
  private float humidity;
  private float pressure;

  public WeatherData() {
    observers = new ArrayList();
  }

  public void registerObserver(Observer o) {
    observers.add(o);
  }

  public void removeObserver(Observer o) {
    int i = observers.indexof(o);
    if(i >= 0) observers.remove(i);
  }

  public void notifyObservers() {
    for (int i = 0; i < observers.size(); i++) {
      Observer observer = (Observer)observers.get(i);
      observer.update(temperature, humidity, pressure);
    }
  }

  public void measurementsChanged() {
    notifyObservers();
  }

  public void setMeasurements(float temperature, float humidity, float pressure) {
    this.temperature = temperature;
    this.humidity = humidity;
    this.pressure = pressure;
    measurementsChanged();
  }

  // other weatherData methods
  // ..
}
```

### 2. Concrete Observer
```java
public class CurrentConditionDisplay implements Observer, DisplayElement {
    private float temperature;
    private float humidity;
    private Subject weatherData;

    public CurrentConditionDisplay(Subject weatherData) {
      this.weatherData = weatherData;
      weatherData.registerObserver(this);
    }

    public void update(float temperature, float humidity, float pressure) {
      this.temperature = temperature;
      this.humidity = humidity;
      display();
    }

    public void display() {
      System.out.println("current conditions: " + temperature 
        + "F degrees and " + humidity + "% humidity");
    }
}
```

***
## Sample

```java
public class WeatherStation {
  public static void main(String[] args) {
    
    // subject
    WatherData weatherData = new WeatherData();

    // observers
    CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay(weatherData);
    StatisticsDisplay statisticDisplay = new StatisticsDisplay(weatherData);
    ForecastDisplay forecastDisplay = new ForecastDisplay(weatherData);

    weatherData.setMeasurements(80, 65, 30.4f);
    // -> "current conditions: 80.0F degrees and 65.0% humidity"
    //    [display of StatisticsDisplay]
    //    [display of ForecastDisplay]
    weatherData.setMeasurements(82, 70, 29.2f);
    // -> "current conditions: 82.0F degrees and 70.0% humidity"
    //    [display of StatisticsDisplay]
    //    [display of ForecastDisplay]
    weatherData.setMeasurements(78, 90, 29.2f);
    // -> "current conditions: 78.0F degrees and 90.0% humidity"
    //    [display of StatisticsDisplay]
    //    [display of ForecastDisplay]
  }
}
```