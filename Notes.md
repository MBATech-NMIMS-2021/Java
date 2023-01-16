# Access Specifiers

1. Private
2. Public
3. Protected

## Polymorphism

1. Compile time Polymorphism (Static Polymorphism)
2. Runtime Polymorphism (Dynamic Method Dispatch)

### Compile Time Polymorphism

- Method Overloading
- Operator OverLoading
- Constructor Overloading

## Overloading

3 types

1. Constructor Overloading
2. Method Overloading
3. Operator

**Please note that in Java, operator overloading is not possible. Only + operator is an exception to this rule as it can be used bw string and int.**

- Functions can't be overloaded based on return type, with same parameters.

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

- This is it's correct version

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

- Functions can be overloaded based on the data types of arguments

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

- Functions can also get overloaded based on the sequence of data types of arguments being passed
- Below is a code with 2 methods, taking 2 arguments, one double, and an int. Still they are getting overloaded

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

- *Constructors*: Special methods for initializing objects
- They are of 2 types

1. Default Constructor (No parameters)
2. Parameterized Constructor (1 or more parameters)

- Constructors can be overloaded based on the data type, and count of arguments mentioned

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