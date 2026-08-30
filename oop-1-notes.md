# OOP 1 — Introduction & Concepts (Java)

Video: [OOP 1 | Introduction & Concepts — Kunal Kushwaha](https://youtu.be/BSVKUk58K6U)

## 1. Why object-oriented programming?

When a program stores many similar entities—such as students, cars, or products—keeping separate variables for every property quickly becomes difficult.

For example, a student record may contain:

```java
int rollNumber;
String name;
float marks;
```

OOP groups related **data** and **behaviour** into one unit: an object.

## 2. Class and object

### Class

A **class** is a logical blueprint or custom data type. It describes:

- Properties/fields: what an entity has
- Methods: what an entity can do

```java
class Student {
    int rollNumber;
    String name;
    float marks;

    void greeting() {
        System.out.println("Hello, my name is " + name);
    }
}
```

The class itself is only a design. It does not represent one particular student yet.

### Object

An **object** is a real instance of a class. It occupies memory and contains its own field values.

```java
Student kunal = new Student();
Student rahul = new Student();
```

`kunal` and `rahul` are two different objects created from the same `Student` blueprint.

Analogy:

```text
Class  → logical construct / blueprint
Object → physical instance / memory representation
```

One class can produce many objects, just as one car design can produce many individual cars.

## 3. Declaring and creating an object

```java
Student student1;             // declaration
student1 = new Student();     // object creation and assignment

// Usually written together:
Student student2 = new Student();
```

Breakdown:

- `Student`: the reference type
- `student2`: a reference variable
- `new`: allocates memory for a new object at runtime
- `Student()`: calls the constructor

The variable does not contain the complete object directly. It stores a reference to the object.

```text
student2  ───────────────►  Student object in heap memory
```

## 4. Fields and the dot operator

The dot (`.`) operator accesses a field or method through an object reference.

```java
kunal.rollNumber = 13;
kunal.name = "Kunal Kushwaha";
kunal.marks = 84.5f;

System.out.println(kunal.name);
kunal.greeting();
```

The same class can hold different values for different objects:

```java
kunal.rollNumber = 13;
rahul.rollNumber = 28;
```

## 5. Constructors

A **constructor** is a special member of a class that runs when an object is created. It is mainly used to initialise the object.

Rules:

- Its name must match the class name.
- It has no return type—not even `void`.
- It runs automatically when `new` creates an object.
- A class can have multiple constructors with different parameter lists.

### Parameterised constructor

```java
class Student {
    int rollNumber;
    String name;
    float marks;

    Student(int rollNumber, String name, float marks) {
        this.rollNumber = rollNumber;
        this.name = name;
        this.marks = marks;
    }
}

Student kunal = new Student(13, "Kunal Kushwaha", 84.5f);
```

`this` refers to the current object. It distinguishes the object’s fields from constructor parameters with the same names.

### Default constructor

If no constructor is written, Java provides a no-argument default constructor. Its fields receive Java’s default values:

```text
int, long, short, byte → 0
float, double          → 0.0
boolean                → false
char                   → '\u0000'
reference types        → null
```

Once you write any constructor yourself, Java no longer supplies the implicit default constructor. Add one explicitly if you still need `new Student()`.

```java
Student() {
    // no-argument constructor
}
```

## 6. Reference variables and assignment

```java
Student one = new Student(1, "A", 80);
Student two = one;
```

This creates **one object and two references**:

```text
one  ─┐
      ├────────► the same Student object
two  ─┘
```

Therefore:

```java
two.name = "Changed";
System.out.println(one.name);  // Changed
```

Assigning one object variable to another copies the reference, not the whole object. To create an independent object, call `new` again or use a copy constructor.

## 7. Primitive types vs reference types

### Primitive variable

Stores a value directly:

```java
int a = 10;
int b = a;
b = 20;

// a is still 10
```

### Reference variable

Stores a reference to an object:

```java
Student a = new Student();
Student b = a;

// a and b refer to the same object
```

The reference can be changed to point somewhere else, but changing a field through either reference changes the shared object.

## 8. `final`

`final` prevents reassignment after initialization.

```java
final int INCREASE = 2;
// INCREASE = 3;  // compilation error
```

A final reference cannot point to a different object:

```java
final Student kunal = new Student();
// kunal = new Student();  // compilation error
```

But `final` does not automatically make the object immutable:

```java
kunal.name = "New name";     // allowed if name is not final
```

So remember:

```text
final reference → reference cannot change
object fields   → may still change
```

## 9. Memory and garbage collection

- Local primitive variables are commonly stored in the stack frame.
- Objects created with `new` live in heap memory.
- Reference variables point to those objects.
- When an object has no reachable reference, it becomes eligible for garbage collection.
- Java’s Garbage Collector (GC) automatically reclaims eligible heap memory; the programmer does not manually free objects.

```java
Student s = new Student();
s = null;
```

After `s = null`, the object may be eligible for GC if no other reference points to it. Eligibility does not mean that GC runs immediately.

## 10. The complete example

```java
class Student {
    int rollNumber;
    String name;
    float marks;

    Student() {
        rollNumber = 0;
        name = "Unknown";
        marks = 0.0f;
    }

    Student(int rollNumber, String name, float marks) {
        this.rollNumber = rollNumber;
        this.name = name;
        this.marks = marks;
    }

    void greeting() {
        System.out.println("Hello, I am " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Student kunal = new Student(13, "Kunal Kushwaha", 84.5f);
        Student other = new Student();

        kunal.greeting();
        System.out.println(kunal.rollNumber);

        Student alias = kunal;
        alias.name = "Updated name";
        System.out.println(kunal.name); // Updated name
    }
}
```

## Quick revision

1. A class is a blueprint; an object is an instance of that class.
2. `new` creates an object and invokes its constructor.
3. A reference variable points to an object; it does not hold the whole object itself.
4. Use `.` to access an object’s fields and methods.
5. Constructors initialize objects and have the same name as the class.
6. `this` refers to the current object.
7. Assigning reference variables copies the reference, so both variables can point to one object.
8. `final` prevents reassignment, but does not necessarily make an object immutable.
9. Unreachable objects become eligible for garbage collection.

## Practice questions

1. What is the difference between a class and an object?
2. What does `new Student()` do?
3. Why does a constructor not have a return type?
4. What is the result of `Student b = a;`?
5. Why does changing `b.name` also change `a.name` when `a` and `b` refer to the same object?
6. What happens to fields when an object is created with a no-argument constructor?
7. What is the difference between `final Student s` and an immutable `Student` object?
8. When does an object become eligible for garbage collection?