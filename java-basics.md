# Learning Java - the basics

## The anatomy of a Java program

Filename: `HelloWorld.java`

The public class must match the filename:

```java
public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello, world!");
  }
}
```

`public static void main(String[] args)` is the main function that Java looks for first to start running the program. It can be written by simply typing `m` in the class and pressing tab in VS Code. In a similar fashion `System.out.println` can be written by simply typing `so` in VS Code and pressing tab.

Java must be compiled with the java compiler: `javac HelloWorld.java`

That will (for now, I guess?) result in a single file called `HelloWorld.class`. It can be run with `java HelloWorld`

## Defining variables

Variables are strongly typed and must be defined with their type:

```java
int age = 30; // Whole numbers in the range +/- 2 billion. Uses 4 bytes of memory
long population = 7000000000; // Whole numbers in the range +/- 9 quintillion (9.2e18). Uses 8 bytes of memory
double price = 14.99; // Supports decimals
char grade = 'A'; // Stores a single character, must use single quotes
String text = "Some text here"; // Stores a text string, must use double quotes
boolean runOnce = true; // Stores a boolean, true/false, should come from a comparison and not be stored directly
```

Output text and numbers on the same line:

```java
int volume = 10;

System.out.println("Volume 1 is " + volume1 + " cubic litres"); // Volume 1 is 10 cubic litres
```

## Math operations

```java
int age = 30;
age++; // Incremenet by one after
age += 2; // Increment by 2
++age; // Increment by one before

int count = 50;
age--; // Decrement by one after
age -= 2; // Decrement by 2
--age; // Decrement by one before

int area = 10;
area *= 10; // Multiply by 10
area /= 5; // Divide by 5
```

Output text and a math operation:

```java
int volume1 = 10;
int volume2 = 50;

System.out.println("The combined volume of 1 and 2 is " + volume1 + volume2);
// The combined volume of 1 and 2 is 1050
System.out.println("The combined volume of 1 and 2 is " + (volume1 + volume2));
// The combined volume of 1 and 2 is 60
```

Numbers are concatenated unless inside parenthesis.

## Type casting

An int can be converted to double, or double can be converted to int by specifying its type before the variable name:

```java
double price = 14.10;
int rounded = (int)price; // Removes decimals from price and stores in 'rounded' variable

int area = 100;
double preciseArea = (double)area; // adds decimals to area and stores in preciseArea. Will be .0 by default
```

Though my personal experimentation has found that the `(type)` isn't required to add. The code compiles and runs just fine without it, no errors, no warnings. It might be about readability and communication of intent though.

## Scanner

Ask for input from the user using Scanner. It needs to be imported from the util class before it can be used:

```java
import java.util.Scanner;

public class Survey {
  public static void main(String[] args) {
    Scanner scan = new Scanner(system.in);
    String name = scan.nextLine();
    int age = scan.nextInt();
    double = price = scan.nextDouble();
    long bigNumber = scan.nextLong();
    scan.close();
  }
}
```

If a `nextLine()` is after a `nextInt(), nextDouble() or nextLong()` it gets skipped. I guess the enter-key isn't accepted by the methods looking for a number, so it's passed on to the nextLine() which makes it seem like it gets skipped. The solution for now is to add a throw-away `nextLine()` but a section on delimiters later will fix this properly.

```java
int age = scan.nextInt();
scan.nextLine();
String name = scan.nextLine();
```

To force English locale so decimals are input with dot instead of comma:

```java
import java.util.Locale;
Scanner scan = new Scanner(System.in).useLocale(Locale.ENGLISH);
```

## Comparison operators

For numbers:

```java
int age = 30;
age > 25; // True if age is greater than 25
age < 35; // True if age is less than 35
age >= 30; // True if age is greater than or equal to 30
age <= 30; // True if age is less than or equal to 30
age == 30; // True if age is 30
age != 30; // True of age is not 30
```

For text:

```java
String sentence = "This is a test";
String sentence2 = "This is a test";

sentence.equals(sentence2); // True since they are identical
!sentence.equals(sentence2); // False since they are identical
```

## if statements

Used to make comparisons. Expects the compared expression to return either true or false. `If` only runs the code in the immediately following curly braces if the expression is true. If there is an else statement that will run if the expression is false. More if statements can be nested with else if, in case more comparisons are wanted:

```java
int cost = 100;

if (cost > 100) {
  System.out.println("Cost is too high");
} else if (cost > 50) {
  System.out.println("Cost is reasonable");
} else {
  System.out.println("Seems too cheap, is it reliable?");
}
```

If statements can contain multiple expressions using AND or OR operators:

```
AND = &&
OR = ||
```

AND returns true if both expressions are true, while OR returns true if either of the expressions are true. In that sense, OR might only need to check the first expression, while AND will have to check both:

```java
int volume = 10;
int amount = 100;

if (volume >= 10 && amount >= 100) {
  System.out.println("True since both expressions are true");
}
if (volume >= 10 || amount >= 200) {
  System.out.println("True because the first expression is true");
}
if (volume >= 20 || amount >= 100) {
  System.out.println("True because the second expression is true");
}
```

## Switch statements

Switch checks a given argument for some values:

```java
int day = 1;
switch (day) {
  case 1: System.out.println("Monday"); break;
  case 2: System.out.println("Tuesday"); break;
  case 3: System.out.println("Wednesday"); break;
  case 4: System.out.println("Thursday"); break;
  case 5: System.out.println("Friday"); break;
  case 6: System.out.println("Saturday"); break;
  case 7: System.out.println("Sunday"); break;
  default: System.out.println("Error! Expected a number between 1 and 7 inclusive");
}
```

The `break` keyword is used to stop processing when a match is found. Without it the following cases would also be run even though they don't match.

## Delimiters

A delimiter is white space that separates input data. So 3 numbers on the same line needs 3 scan.nextInt to capture them. A new method here is simply `scan.next()` which picks up words on the same line separated by white space. As we've seen `scan.nextLine()` reads the entire line, including the white space so when it comes after a nextInt() it picks up the white space after the number.

## Functions

A function in Java is defined like this: `public void singChorus( ... ) { ... }`

`public` means the function can be called from anywhere. I've seen private used as well, which I guess means it can only be called from within the class or object, but we'll get to that.

`void` means the function doesn't return anything.

Then there's the function parameters, which can be empty or contain for instance `int number` if it expects a number of type int. Then the function code follows inside the curly braces.

From that we should understand that `main` is also a function, and the one Java looks for to start the program. It is defined as `static` which means any function calls we make from within it also has to be static functions.

So this doesn't compile:

```java
public class Chorus {
  public static void main(String[] args) {
    singChorus();
  }
  public void singChorus() {
    System.out.println("Singing the chorus");
  }
}
```

By adding the `static` keyword to the function, like for main fixes the problem and it compiles. For now all functions have to be static, we'll learn more about why when we get to Object Oriented Programming later.

Function names should follow the camel case naming convention. Functions will also be referred to as methods. (Learnt from JavaScript that functions in objects are called methods, and in Java, everything is in an object)

## Function parameters

Parameters are values that the function expects to receive.

```java
public void calculateRectangle(double length, double width) {
  System.out.println(length * width);
}
```

Calling this function without parameters won't compile.

## Function return values

The function shouldn't handle the calculated value itself, but return it to what called the function. The return type in the function definition must match the returned value.

```java
public double calculateRectangle(double length, double width) {
  double area = length * width;
  return area;
}
```

It doesn't seem like we need the `area` variable here, but we can just return `length * width` and it seems to work fine.

## Doc comments

Comments that document your functions:

```java
/**
 * Function name: fahrenheitToCelsius - convers fahrenheit to celsius
 * @param   fahrenheit (double)
 * @return  celsius   (double)
 *
 * Inside the function:
 *  1. return the celsius temperature.  C = (F - 32) * 5/9
 */
```

## Scope

Variables are block scoped, so can't be accessed outside the block they're defined in.

## Built-in functions

`println` is an example of a built-in function. It isn't local to our class, so we need to prefix it with `System.out` to specify the class it comes from.

Other examples are `log`, `sin` or `cos` which are built-in math functions, in the `Math` class. They usually expect a double as argument and return a double with the result:

```java
double somethingLog = Math.log(101.53);
double somethingSin = Math.sin(1.2);

// Math.pow expects two arguments, calculates the first raised to the power of the second
double somethingPow = Math.pow(2, 4);

// Math.random expects no arguments, return a number between 0 and less than 1
double somethingRandom = Math.random();
```

To find other build-in functions, see docs at Oracle.

## For loops

```java
for (int i = 0; i < 10; i++) {
  // Do something 10 times
}
```

## While loops

Runs as long as the condition is true

```java
boolean flag = 10 > 5;
while (flag) {
  System.out.println("It ran!");
  flag = 10 < 5;
}
```

## Break and continue

Continue skips any code after it and returns to the top of the current loop. This only prints every other number:

```java
for (int i = 0; i <= 10; i++) {
  if (i % 2 != 0) {
    continue;
  }
  System.out.println(i);
}
```

Break exits the loop when encountered. So if `break` was used instead of `continue` above, only 0 would be printed before the loop would exit.

## Arrays

Arrays can only hold one type of items, as the type have to be specified. To create one array of integers and one of strings:

```java
int[] integers = {1, 2, 3};
String[] names = {"Jane", "Joe", "Anna"};
```

The integers name doesn't actually hold the array, but a reference to it. That means it can't just be printed like a normal variable. Just printing the arrays results in

```
[I@d716361
[Ljava.lang.String;@6ff3c5b5
```

for the integer and string array respectively.

Elements have to be accessed by their index:

```java
int first = integers[0];
String last = names[2];
```

Accessing an element that doesn't exist compiles, but crashes at run-time so beware.

Loop through an array with a for-loop:

```java
for (int i = 0; i < array.length; i++) {
  System.out.println(array[i]);
}
```

A popular way to get the last element of an array: `println (array[array.length-1]);`

To update an element in an array, simply set the element at `array[index]` to the new value

Arrays can be printed with `.toString()` instead of looping through them. This method is on the Arrays object and takes the array to convert to string as an argument:

```java
import java.util.Arrays;
String[] array = {"Item 1", "Item 2", "Item 3", "Item 4"};
String arrayString = Arrays.toString(array);
System.out.println(arrayString);
```

The length of an array can't be resized after it has been created, instead a new array have to be created with the new size:

```java
String[] newArray = new String[5];
int i;
for (i = 0; i < array.length; i++) {
  newArray[i] = array[i];
}
newArray[i] = "Item 5";
```

A string can't be set to an array without specifying the index the string should be at. So this won't work:

```java
String[] variable = Arrays.toString(array);
```

But this will:

```java
String[] variable = new String[2];
variable[0] = Arrays.toString(array);
```

## Array reference trap

Multiple arrays can point to the same values:

```java
int[] numbers = {1, 2, 3, 4};
int[] numbers2 = numbers;
System.out.println(numbers);  // [I@d716361
System.out.println(numbers2); // [I@d716361
```

Changing the values through the numbers2 variable also changes what you get when you access the numbers variable.

Instead of having to use loops to copy an array we can use `Arrays.copyOf`:

```java
int[] numbers = Arrays.copyOf(numbers, numbers.length);
```

## 2D arrays

Create a new, empty 2D array with 3 rows and 4 columns, then add values to it and access them

```java
int[][] integers = new int[3][4];
integers[0][0] = 0;
integers[0][1] = 1;
integers[0][2] = 2;
integers[0][3] = 3;
integers[1][0] = 10;
integers[1][1] = 11;
integers[1][2] = 12;
integers[1][3] = 13;
System.out.println(Arrays.toString(integers[0]));
System.out.println(integers[0][0]);
System.out.println(integers[1][0]);
System.out.println(integers[1][3]);
```

Or create and initialize it like this:
```java
int[][] grades = {
  {1, 2, 3, 4},
  {3, 4, 5, 6},
  {5, 6, 7, 8}
}
```

The length of a 2D array is determined by the number of rows. The length of a row is determined by the number of elements (columns):

```java
int[][] integers = new int[3][4]; // 3 rows, 4 columns
System.out.println(integers.length); // 3
System.out.println(integers[0].length); // 4
System.out.println(integers[1].length); // 4
```

## Looping through 2D arrays

```java
for (int i = 0; i < integers.length; i++) {
  for (int ii = 0; ii < integers[i].length; ii++) {
    System.out.println(integers[i][ii] + "");
  }
  System.out.print("\n");
}
```

Adding a switch statement to describe the rows:

```java
for (int i = 0; i < integers.length; i++) {
  switch (i) {
    case 0: System.out.print("Elements in row 0: "); break;
    case 1: System.out.print("Elements in row 1: "); break;
    case 2: System.out.print("Elements in row 2: "); break;
    default: System.out.println("Array contained more rows that we anticipated, exiting!");
      System.exit(-1);
  }
  for (int ii = 0; ii < integers[i].length; ii++) {
    System.out.print(integers[i][ii] + " ");
  }
  System.out.print("\n");
}
```

Or we could store the description in another array, and look them up there:

```java
String[] names = {
  "Elements in row 0: ", 
  "Elements in row 1: ",
  "Elements in row 2: "
};
for (int i = 0; i < integers.length; i++) {
  System.out.print(names[i]);
  for (int ii = 0; ii < integers[i].length; ii++) {
    System.out.print(integers[i][ii] + " ");
  }
  System.out.print("\n");
}
```

Return a new array with `return new int[] { 1, 2, 3 };`
