## Why JAVA

-   Unlike C++ Java doesn't support multiple inheritance because of diamond problem.
-   Multiple inheritance can still be done through interfaces.
-   Multi level inheritance is possible.

class C extends B extends A is not possible

A->B->C level

-   Java doesn't allow programmers to deal with memory directly which makes it easier, and secured.

## ArrayList

```java
import java.util.Scanner;
import java.util.ArrayList;

class C{
    public static void main (String[] args){
        ArrayList<Integer> sam = new ArrayList<Integer>();
        sam.add(1);
        System.out.println(sam);
    }
}
```

## Access Specifiers

1. Private
2. Public
3. Protected
4. Default (Not a keyword)

## Polymorphism

Polymorphism is the ability of an object to take multiple forms.

1. Compile time Polymorphism (Static Polymorphism)
2. Runtime Polymorphism (Dynamic Method Dispatch)

### Compile Time Polymorphism

-   Method Overloading
-   Operator OverLoading
-   Constructor Overloading

## Overloading

3 types

1. Constructor Overloading
2. Method Overloading
3. Operator

**Please note that in Java, operator overloading is not possible. Only + operator is an exception to this rule as it can be used bw string and int.**

-   Functions can't be overloaded based on return type, with same parameters.

```java
class OverLoading {
    int add(int a, int b) {
        return a + b;
    }

    void add(int a, int b) {
        System.out.println(a + b);
    }
}
```

The above code is incorrect.

-   This is it's correct version

```java
class OverLoading {
    int add(int a, int b) {
        return a + b;
    }

    void add() {
        System.out.println(1+2);
    }
}
```

-   Functions can be overloaded based on the data types of arguments

```java
class OverLoading {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b){
        return a + b;
    }
}
```

-   Functions can also get overloaded based on the sequence of data types of arguments being passed
-   Below is a code with 2 methods, taking 2 arguments, one double, and an int. Still they are getting overloaded

```java
class OverLoading {
    int add(int a, double b) {
        return a;
    }
    int add(double a, int b) {
        return b;
    }
}
```

-   _Constructors_: Special methods for initializing objects
-   They are of 2 types

1. Default Constructor (No parameters)
2. Parameterized Constructor (1 or more parameters)

-   Constructors can be overloaded based on the data type, and count of arguments mentioned

```java

class OverLoading {
    OverLoading(int a, int b) {

    }
    OverLoading(int a) {

    }
    OverLoading(double a) {

    }
}

```

## Polymorphism, Upcasting

If reference variable of parent class refers to the object of Child class, it's called Upcasting.

```java
import java.util.Scanner;
import java.util.ArrayList;

class SuperClass {
    int a = 10;
    int b = 20;
}

class ChildClass extends SuperClass {
    int a = 30;
    int b = 40;
}

class Program {
    public static void main(String[] args) {
        SuperClass superClass = new SuperClass();
        ChildClass childClass = new ChildClass();
        SuperClass upcastTrial1 = new ChildClass();
        // ChildClass upcastTrial2 = new SuperClass(); Compilation Error, Incompatible types

        System.out.println(upcastTrial1.a);
        System.out.println(superClass.a);
        System.out.println(childClass.a);
    }
}
```

**Point to note**

The following program will generate an error:

```java
import java.util.Scanner;
import java.util.ArrayList;

class SuperClass {
    int a = 10;
    int b = 20;
}

class ChildClass extends SuperClass {
    int a = 30;
    int b = 40;
}

class Program {
    public static void main(String[] args) {
        SuperClass superClass = new SuperClass();
        ChildClass childClass = new ChildClass();
        SuperClass upcastTrial1 = new ChildClass();
        // ChildClass upcastTrial2 = new SuperClass(); //Error

        childClass = upcastTrial1;

        System.out.println(upcastTrial1.a);
        System.out.println(superClass.a);
        System.out.println(childClass.a);
    }
}
```

Reason this program generates an error is the following

In the line `childClass = upcastTrial1;` the data type of RHS and LHS are not equal, hence an effort is made by the compiler to perform implicit type casting.

Now the type of RHS is `SuperClass`, and of LHS is Child Class. Compiler tries to convert SuperClass to Child class, but this is not possible as a parent class can't be type casted to a child class.

Vice versa is true, child class can be type casted to a parent class. Hence this program works correctly

```java
import java.util.Scanner;
import java.util.ArrayList;

class SuperClass {
    int a = 10;
    int b = 20;
}

class ChildClass extends SuperClass {
    int a = 30;
    int b = 40;
}

class Program {
    public static void main(String[] args) {
        SuperClass superClass = new SuperClass();
        ChildClass childClass = new ChildClass();
        SuperClass upcastTrial1 = new ChildClass();
        // ChildClass upcastTrial2 = new SuperClass(); //Error

        upcastTrial1 = childClass;

        System.out.println(upcastTrial1.a);
        System.out.println(superClass.a);
        System.out.println(childClass.a);
    }
}
```

Now kindly check the following code's output

```java
import java.util.Scanner;
import java.util.ArrayList;

class SuperClass {
    int a = 10;
    int b = 20;
}

class ChildClass extends SuperClass {
    int a = 30;
    int b = 40;
}

class Program {
    public static void main(String[] args) {
        SuperClass superClass = new SuperClass();
        ChildClass childClass = new ChildClass();
        SuperClass upcastTrial1 = new ChildClass();
        // ChildClass upcastTrial2 = new SuperClass(); //Error

        System.out.println(upcastTrial1.a);
        System.out.println(superClass.a);
        System.out.println(childClass.a);
        System.out.println("   ");

        upcastTrial1 = childClass;

        System.out.println(upcastTrial1.a);
        System.out.println(superClass.a);
        System.out.println(childClass.a);
    }
}
```

Even after the assignment, the output remains same as before. This happened because `upcastTrial1` which was updated still is the instance of superclass, and event the RHS `childClass` still is an instance of child class, hence output is justified.

## Overriding

-   Methods in Java can be overloaded.
-   The following code

```java
import java.util.Scanner;
import java.util.ArrayList;

class SuperClass {
    int num1 = 10;
    int add(int a, int b) {
        return a + b;
    }
}
class ChildClass extends SuperClass {
    int num1 = 20;
    int add(int a, int b) {
        return (a + b) * 2;
    }
}

class Program {
    public static void main(String[] args) {
        SuperClass superClass = new SuperClass();
        ChildClass childClass = new ChildClass();
        SuperClass upCastTrial1 = new ChildClass();

        System.out.println(superClass.add(2,3));
        System.out.println(childClass.add(2,3)); // Using the updated add fn
        System.out.println(upCastTrial1.add(2, 3)); // Using the updated add fn

        System.out.println("===============");

        System.out.println(superClass.num1);
        System.out.println(childClass.num1);
        System.out.println(upCastTrial1.num1);
    }
}
```

-   Here you can notice various things

1. Methods can be overriden.
2. Overriden methods will only get used when instance of child class is created, or Superclass instance refers to Child Class.
3. Variables can't be overriden.
4. So updated variable value will only be visible to instance of Child Class.

## Super

whenever a subclass needs to refer to immediate sperclass, it can do so by the use of super

Sub class can call parent class's constructor.

Super is a keyword, can be used to access, instance variable of parent class

Compiler always call super class constructor by default in parent child relationship

super contructor line has to the 1st line of any constructor

We can call constructors from another constructors a method cannot call constructor

If we don't call constructor explicity, then the default constructor with no parameters gets called.

```java
class SuperClass {
    SuperClass() {
        System.out.println("Executing Super class");
    }
}

class ChildClass extends SuperClass {
    ChildClass() {
        System.out.println("Executing Child Class");
    }
}

public class a {
    public static void main(String[] args) {
        System.out.println("Sam");

        ChildClass childClass = new ChildClass();
    }
}
```

## Data Abstraction

- Data Abstraction is the property by virtue of which only the essential details are displayed to the user.
- In layman words, it's the way to write different code for different classes/fns (that mostly is intended to perform similar thing). We are writing different code because we might not wanna do the same thing for all the classes.

There are 2 ways in java we can perform data abstraction

1. Abstract class
2. Interfaces

### Abstract Class

```java
abstract class B {
    abstract void display();
}

class A{
    public static void main (String[] args){
    }
}
```

- You can't create instances of an abstract class.
- We can have abstract class without any abstract method.
- Methods in abstract class can't be final. (As this will offend the very purpose of data abstraction)
- If a class contains atleast 1 abstract method, then that class should be compulsorily be declared abstract.
- If we create child classes of an abstract class, then it must compulsorily override all abstract methods of parent abstract class.

```java
abstract class B {

    // final int a = 5;
    abstract void a();
    void b(){}
}

class C extends B {
    // Without the fn of a, program won't run
    void a() {
        System.out.println("Runnin");
    }
}

class A{
    public static void main (String[] args){
    }
}
```

### Interfaces

- All methods need to have **no body**.

```java
interface species {
    public void speciesDetails(); // Dont put {}, no body

    // public void a(){};
}

class Humans implements species {
    public void speciesDetails() {
        System.out.println("I am a human");
    }
}

class C {
    public static void main(String[] args) {
        Humans human = new Humans();
        human.speciesDetails();
    }
}
```

- All variables in an interface are by default public static and final (whose value can't be changed).
- Interfaces even with empty body is not allowed.

## Super

- By calling `super` in the first line of the constructor function of inherited class.
- We can also call methods of parent class using `super.methodName();`.

## Strings

- `string.length()` Returns the length of string.
- `string.toUpperCase()` Returns string with all characters in upper case.
- `string.toLowerCase()` Returns the strings with all characters in lower case.
- `string.indexOf("someString")` Returns the starting index of `someString` from string. Returns -1 if the sub string is not found.
- To convert string to integer, use `int number = Integer.parseInt("123");`