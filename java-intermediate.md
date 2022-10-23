# Learning Java - intermediate

Things that are possibly more advanced than basics, but not purely OOP either goes here.

## Conditional assignment - ternary operator

Like JavaScript Java has a conditional assignment operator, also called ternary operator.

```java
String result = ( 5 > 2) ? "Larger" : "Smaller";
```

## Exception handling

Exceptions are failures that can crash your program. Handling exceptions involves catching 'checked' exceptions and finding 'unchecked' exceptions.

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

