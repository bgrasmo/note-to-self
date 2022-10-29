# Learning Java - intermediate

Things that are possibly more advanced than basics, but not purely OOP either goes here.

## Conditional assignment - ternary operator

Like JavaScript Java has a conditional assignment operator, also called ternary operator.

```java
String result = ( 5 > 2) ? "Larger" : "Smaller";
```

## Exception handling

Exceptions are failures that can crash your program. Handling exceptions involves catching 'checked' exceptions and finding 'unchecked' exceptions.

## Checked exceptions

A 'checked' exception is a failure the program cannot control, so Java will force you to catch those. Examples of these failures are trying to connect to a website or a database, accessing a missing file or trying to access something in a database. Code is more likely to fail if it interacts with outside resources.

Code that is likely to fail will throw a checked exception which Java forces you to handle.

```java
public void loadFile() throws FileNotFoundException {

}
```

Like for Javascript we have to wrap code like that in a try/catch block:

```java
try {
  loadFile();
} catch (FileNotFoundException e) {
  System.out.println(e.getMessage());
}
```

Adding code to read in a file results in code that won't compile unless we handle the exception of the file not being found:

```java
import java.io.FileInputStream;
FileInputStream fis = new FileInputStream("Greetings.txt");
```

The things our program can't control is if the filename entered was wrong, or the file for some other reasons doesn't exist. So we have to add the try/catch block around it, like shown above. We can use debugging in the editor to step into the `FileInputStream` method for instance, and see the exception(s) it throws. (Though hovering over the line in the editor will show the same.)

We can use the Scanner to not only read input entered manually by the user of the program, but also from files:

```java
FileInputStream fis = new FileInputStream("Greetings.txt");
Scanner scan = new Scanner(fis);
while (scan.hasNextLine()) {
  System.out.println(scan.nextLine());
}
scan.close();
```

We can handle exceptions in two ways, either add try/catch inside the function for the code that can file, or we can mark that the function can fail and then handle that when we cann the function:

Inside the function:

```java
public class ReadingFiles {
  public static void main(String[] args) {
    try {
      FileInputStream fis = new FileInputStream("Greetings.txt");
      Scanner scan = new Scanner(fis);
      while (scan.hasNextLine()) {
        System.out.println(scan.nextLine());
      }
      scan.close();
    } catch (FileNotFoundException e) {
      System.out.println(e.getMessage());
    }
  }
}
```

Marking that the function can fail and handling it outside the function:

```java
public class ReadingFilesTwo {
  public static void main(String[] args) {
    try {
      loadData("Greetings.txt");
    } catch (FileNotFoundException e) {
      System.out.println(e.getMessage());
    }
  }

  public static void loadData(String name) throws FileNotFoundException {
    FileInputStream fis = new FileInputStream(name);
    Scanner scan = new Scanner(fis);
    while (scan.hasNextLine()) {
      System.out.println(scan.nextLine());
    }
    scan.close();
  }
}
```

Malformed URL exception:

```java
import java.net.MalformedURLException;
import java.net.URL;

public class ParseURL {
  public static void main(String[] args) {
    try {
      URL url = new URL("https://www.google.com");
    } catch (MalformedURLException e) {
      System.out.println(e.getMessage());
    }
  }
}
```

Again we can do this in two ways, with having try/catch in the function that can fail as shown above, or marking that it can fail with `MalformedURLException`. The last is for now left as an exercise to the reader.

To catch multiple exceptions we can have multiple function calls that can fail in a single try block, but we need multiple catch blocks to catch the errors given they are named differently.

## Unchecked exceptions

These happens during the runtime, like the nullPointerException we've already encountered. While we need to handle checked exceptions so they won't happen, we need to fix unchecked exceptions when encountered.

Unchecked exceptions are the result of badly written code. They should never be 'catched' as that is 'sweeping the problem under the rug'. Instead fix the code so it doesn't fail.

Common unchecked exceptions are `ArrayIndexOutOfBoundsException`, `NullPointerException`, `IllegalArgumentException`, `InputMismatchException` and `IllegalStateException`.

To avoid the array exception you might need to check the array length before you access it For nullpointer, check if the value is null with the `==` comparison before accessing it. Using .equals(null) will not work but will always throw the nullpointer exception we're trying to avoid instead.

For input mismatch, which relates to the scanner, we can for instance check if there is an int comming up, if that's the input we're expecting. If not, grab the input with next and show a message stating it was wrong:

```java
Scanner scan = new Scanner(System.in);
System.out.print("Please enter a number: ");
if (scan.hasNextInt()) {
  System.out.println(scan.nextInt());
} else {
  scan.nextLine();
  System.out.println("Not a number!");
}
scan.close();
```

This can be put in a `while (true) {}` loop running forever unless the user inputs what we expect, then we can break the loop.

## Throwing unchecked exceptions

But first we start with creating a 'package'. When a class file resides in a different folder than the others we have to specify its folder by adding `package <foldername>;` to the top of it. Then we need to import said file in our main directory with `import <foldername>.<Classname>;`. To import every classfile in a folder we can use `*` instead of classname.

The reason for throwing unchecked exceptions is to prevent the caller from misusing methods and/or constructors from our classes. The most common exceptions to throw are the remaining two of the five listed above, namely: `IllegalArgumentException` and `IllegalStateException`.

## Illegal argument exception

An example of someone misusing a method or constructor is if they pass in blanks or null instead of actual arguments:

```java
Employee stocker = new Employee("  ", null);
Employee assistManager = new Employee("John", "  ");
Employee manager = new Employee(null, "  ");
```

To throw an exception in these cases we can check for the unwanted values and then throw the exception:

```java
public Employee(String name, String position) {
  if (name == null || name.isBlank() || position == null || position.isBlank()) {
    throw new IllegalArgumentException("Name or position cannot be null or blank");
  }
}
```

Shouldn't we add that this constructor can throw an exception, or will that only lead to a try/catch block being required which is something we don't want here? I would guess the last part, though this wasn't explained.

The copy constructor usually doesn't need to throw exceptions if we have safeguards in place when originally creating the objects. If the user passes `null` to the copy constructor, Java will be throwing a nullpointer exception so we don't have to do anything.

## Illegal state exception

These are thrown when an object calls a method with an illegal state, or in other words, if an object isn't properly initialized before calling one of its methods.

An example could be a store object with an open method that shouldn't be called if it doesn't have any of the employees from above. The example shown creates the employees and the new store object, but doesn't set any employees in the store.

```java
public class Store {
  public void open() {
    for (int i = 0; i < employees.length; i++) {
      if (employees[i] == null) {
        throw new IllegalStateException("You must be fully staffed before opening the store.");
      }
    }
  }
}
```

In other words the 'setEmployees' method must be called before 'open' can be called:

```java
// main:
Store store = new Store();
store.setEmployee(0, stocker);
store.setEmployee(1, assistManager);
store.setEmployee(2, manager);
store.open();

// class Store:
Employee[] employees;

public void setEmployees(int index, Employee employee) {
  this.employees[index] = new Employee(employee);
}
```

