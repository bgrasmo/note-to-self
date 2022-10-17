# Learning Java - Object Oriented Programming

## Plan your code around objects

1. Look for <b>objects</b> (things)
2. Look for <b>fields</b> that describe each object
3. Look for <b>actions</b> the object can perform

An object is a thing, something that can be seen or described like a car dealership or a car. Fields describe the object, for instance make, model, price, year, color, number of doors and so on. Actions describe what the object can do, like drive.

```java
Car nissan = new Car("Nissan", 5000, 2020, "red");
nissan.drive();
Car dodge = new Car("Dodge", 11000, 2019, "blue");
dodge.drive();
```

## The class

The class is the blueprint from which you can create objects. Create a file `Car.java`:

```java
public class Car {
  String make;
  double price;
  int year;
  String color;
}
```

## Create object from class

'Car' is the class you're creating the object from. Nissan here is the variable name.

Create a file `Main.java` with the main method. In it, add the following:

```java
Car nissan = new Car();
System.out.println(nissan.make);
System.out.println(nissan.price);
System.out.println(nissan.year);
System.out.println(nissan.color);
```

Interestingly, there seem to be no need to import or specify the Car.java file in anyway. Simply compiling Main.java has java building two class files, one called main and one called car, and running just Main works. This was not explained at all.

Objects can be updated with the dot syntax:

```java
nissan.make = "Nissan";
nissan.price = 5000;
nissan.year = 2020;
nissan.color = "red";
```

Or as shown previously, properties can be populated when the object is instantiated with the constructor.

If a class has fields, it needs a constructor, getters and setters.

## The constructor

The constructor runs after you create an object and is a method that shares the name of the class you are in. So for the Car class above it would look like this:

```java
public Car(String make, double price, int year, String color) {
  // Some code here
}
```

Since the constructor has 4 parameters, we need to have 4 arguments when we call it in the main method with the `new` keyword.

```java
Car nissan = new Car("Nissan", 5000, 2020, "red");
```

Introducing `this` which means the current object, and it helps with distinguishing between fields and parameters. In objects, fields and the objects constructor parameters usually have the same name. If we just reference `make` for instance, java looks at the "closest one" and that could be the parameter. While `this` points to the current object, when we reference `this.make` we reference the field in the object, and not the parameter in the constructor or method.

To finish the constructor:

```java
public class Car {
  String make;
  double price;
  int year;
  String color;

  public Car(String make, double price, int year, String color) {
    this.make = make;
    this.price = price;
    this.year = year;
    this.color = color;
  }
}
```

## Public vs Private

Methods and constructors are public, as they should be accessible from anywhere. Fields however should be private as we should not have direct access to them outside of their class. They're set private by adding the keyword in front of them:

```java
private String make;
private double price;
private int year;
private String color;
```

If they had not been set private we would access the field directly, and that can be dangerous. By making them private, we will instead have to access a copy of the value with getters and setters.

## Getters

Since fields are now private, we can't access them from the outside. That means we have to create a getter to return a copy of it instead. A getter is simply a method that returns a fields value:

```java
public String getMake() {
  return this.make;
}
```

Then in main we have to call the getter instead of trying to access the field directly:

```java
System.out.println(nissan.getMake());
```

## Setters

Since we need getters to get the value when the fields are private, we need setters to set a value:

```java
public void setMake(String make) {
  this.make = make;
}
```

Now we can set the make value in the nissan object, and I guess we don't risk setting something in the original car object since there is some reference thing going on here.

```java
nissan.setMake("Nissan A1");
```

## Reference trap

If there are many references to one object, one of them could accidentally update some value for every other reference. Don't set a class variable equal to each other to avoid this. `Car nissan2 = nissan;` is the problem, avoided with using `Car nissan2 = new Car();`

The same applies to arrays. use `Arrays.copyOf` to make a new copy of the array to avoid this.

## Copy constructor

To avoid having to input the same arguments twice for `nissan2` we can use a copy constructor that copies an existing object for us.

Having more than one constructor is called constructor overload.

You can have as many constructors as you want, each having the same name, but having different parameters. Java will then look at the arguments sent to decide what constructor to call.

Send an existing object into a constructor having only one parameter of type Car and call it `source`. This will contain a reference to our original object and we can use it to copy the values:

```java
Car nissan2 = new Car(nissan);

public Car(Car source) {
  this.make = source.make;
}
```

## Actions

An action is a method, something the object can do. So for a car object, it can drive:

```java
public void drive() {
  System.out.println("Driving the car you bought out of the dealership");
  System.out.println("The car being a " + this.make);
}
```

When adding a new field to an object, remember to update the constructor(s), getters and setters. Here we send in an array, which means we have to use the copyOf method otherwise we would just reference the original array:

```java
public class Car {
  //...
  String[] parts;

  public Car(String make, double price, int year, String color, String[] parts) {
    //...
    this.parts = Arrays.copyOf(parts, parts.length);
  }
}
```

Remember to also return an array copy in the getter, otherwise it will return a reference, and make a copy in the setter to avoid setting a reference.

```java
public String[] getParts() {
  return Arrays.copyOf(this.parts, this.parts.length);
}
public void setParts(String[] parts) {
  this.parts = Arrays.copyOf(parts, parts.length);
}
String[] parts = {"Winter tires", "keys"};
Car nissan = new Car("Nissan", 5000, 2020, "midnight blue", parts)
Car nissan2 = new Car(nissan);
nissan2.setParts(new String[] {"tires", "filter"});
```

## toString

We can change the behavior of the toString method:

```java
public String toString() {
  return "Make: " + this.make + ".\n"
    + "Price: " + this.price + ".\n"
    + "Year: " + this.year + ".\n"
    + "Color: " + this.color + ".\n"
    + "Parts: " + Arrays.toString(parts) + ".\n";
}
```

Normally when printing an object the class and hashCode will be printed. But if we've added a toString method to our class, that will be called instead. This is true for every class that models an object.

We can create a dealership class to manage the cars:

```java
public class Dealership {
  private Car[] cars;

  // Constructor, runs when ... new Dealership is called
  public Dealership() {
    this.cars = new Car[3];
    System.out.println(Arrays.toString(this.cars));
  }
  // Set one car in the array, have to specify index otherwise we would have to send a full array each time
  // This will run the copy constructor in the car object
  public void setCar(Car car, int index) {
    this.cars[index] = new Car(car);
  }
  public Car getCar(int index) {
    return new Car(this.cars[index]);
  }
}
```

In main:

```java
Dealership dealership = new Dealership();
dealership.setCar(nissan, 0);
```

This means we can have arrays with more advanced content than just single types like int or String.

Adding a 'sell' action which involves the customer driving away with the car:

```java
public void sell(int index) {
  this.cars[index].drive();
  this.cars[index] = null;
}
```

Could the `drive` method be called with an index instead to perform the same action? Need to test, though it seems this way of calling it is how it's supposed to be. See search method below

Searching for a car:

```java
public String search(String make, int budget) {
  for (int i = 0; i < this.cars.length; i++) {
    if (this.cars[i].getMake().equals(make) && this.cars[i].getPrice() <= budget) {
      System.out.println("We found a match!");
    }
    
  }
  return "Sorry, we couldn't find any cars.";
}
```

This however causes a nullPointerException, because we sold a car and set index 2 to null. We can't use the dot syntax on a null object, so this crashes.

In other words we need to check if the object is null before performing any furhter action.

```java
if (this.cars[i] =0 null) {
  continue;
} else if (the search checks here) {
  System.out.println("We found a match!");
}
```

## Primitive vs class type

Almost everytything in Java is an object.

Primitives store a value directly, like `int a = 15`. They represent a value directly, they cannot be null and they have no methods.

Class types, which are also known as reference types, are classes that you can create objects from. They store a reference that points to an object, it can be null, and it can have methods.

The `String` type is a class type, and a hint to that is it starts with a capital letter, as oposed to `int`, `double`, `boolean` and so on. Class names starts with a captial letter as we've learned before. So when we define a string variable we're actually creating an object of the string class. If we set one string equal to another, they will be identical as they will share the same reference. However, if we assign a new value to either of them it creates a brand new string object, so there is no reference trap here.

```java
String word1 = "Hello";
String word2 = word1;
System.out.println("word1: " + word1.hashCode()); // 69609650
System.out.println("word2: " + word2.hashCode()); // 69609650
word2 = "goodbye";
System.out.println("word1: " + word1.hashCode()); // 69609650
System.out.println("word2: " + word2.hashCode()); // 207022353
```

This behavior is typical for 'immutable' class types such as string. More about that later.

A string can be turned into a character array with `.toCharArray()`:

```java
char[] charArray = word1.toCharArray();
```

The 'scanner' for reading input from the commandline is also a class type, so it can be null and it has methods we've already used: `nextInt()`, `nextLine()` and so on.

As mentioned, primitive types cannot be `null` as it only applies when memory size is not fixed, and primitive types have a fixed memory size. For instance an int is 4 bytes, a long is 8 bytes. Objects don't have a fixed memory size as their size depend on what they contain.

Arrays are also objects, as when we create a new array we create a new object of the array class.

