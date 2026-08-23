# SystemVerilog_OOP

---

## Description

This repository demonstrates **Object-Oriented Programming (OOP) in SystemVerilog**. OOP provides a structured approach to building **modular, reusable, scalable, and maintainable verification environments**.

The examples focus on **classes, objects, inheritance, encapsulation, polymorphism, abstraction, and object copying**, which are fundamental concepts for SystemVerilog-based verification and UVM.

---

## Topics Covered

* SystemVerilog Classes
* Objects and Handles
* Encapsulation
* Inheritance
* Method Overriding
* `super` keyword
* Polymorphism
* Abstraction
* Static Members
* Handle Assignment
* Shallow Copy
* Deep Copy
* Downcasting using `$cast()`
* Automatic Object Lifetime Management

---

## Classes

A **class** is a user-defined data type that acts as a blueprint for creating objects. It encapsulates **properties (data)** and **methods (behavior)** within a single unit.

### Example

```systemverilog
class Packet;

    int data;
    int address;

    function void display();
        $display("Data = %0d, Address = %0d", data, address);
    endfunction

endclass
```

---

## Objects and Handles

An **object** is an instance of a class created dynamically using the `new()` constructor.

A **handle** is a reference used to access the object.

```systemverilog
Packet pkt;

initial begin
    pkt = new();

    pkt.data    = 100;
    pkt.address = 10;

    pkt.display();
end
```

---

## Encapsulation

**Encapsulation** combines data and methods within a class and controls access to class members using access modifiers.

### Access Modifiers

| Modifier    | Accessibility                                   |
| ----------- | ----------------------------------------------- |
| `public`    | Accessible from anywhere                        |
| `protected` | Accessible within the class and derived classes |
| `local`     | Accessible only within the declaring class      |

### Example

```systemverilog
class Packet;

    local int data;

    function void set_data(int value);
        data = value;
    endfunction

    function int get_data();
        return data;
    endfunction

endclass
```

---

## Inheritance

**Inheritance** allows a derived class to reuse and extend the properties and methods of a base class.

SystemVerilog uses the `extends` keyword for inheritance.

```systemverilog
class Parent;
    int data;

    function void display();
        $display("Parent Class");
    endfunction
endclass


class Child extends Parent;

    function void show();
        $display("Child Class");
    endfunction

endclass
```

---

## `super` Keyword

The `super` keyword is used to access members or methods of the parent class.

```systemverilog
class Child extends Parent;

    function void display();
        super.display();
        $display("Child Class");
    endfunction

endclass
```

It is also commonly used to call the parent constructor.

```systemverilog
function new(int value);
    super.new(value);
endfunction
```

---

## Polymorphism

**Polymorphism** allows a base-class handle to refer to an object of a derived class.

Runtime polymorphism is achieved using **virtual methods**.

```systemverilog
class Parent;

    virtual function void display();
        $display("Parent");
    endfunction

endclass


class Child extends Parent;

    function void display();
        $display("Child");
    endfunction

endclass


Parent p;
Child  c;

initial begin
    c = new();
    p = c;

    p.display();
end
```

### Output

```text
Child
```

---

## Abstraction

**Abstraction** hides implementation details and defines an interface that derived classes must implement.

SystemVerilog supports abstraction through **virtual classes** and **pure virtual methods**.

```systemverilog
virtual class Shape;

    pure virtual function void area();

endclass
```

A derived class must implement the pure virtual method.

```systemverilog
class Rectangle extends Shape;

    function void area();
        $display("Calculating Rectangle Area");
    endfunction

endclass
```

---

## Static Members

A `static` class member is shared among **all objects of the class**.

```systemverilog
class Counter;

    static int count;

    function new();
        count++;
    endfunction

endclass
```

The same `count` variable is shared by every `Counter` object.

---

## Object Copying

SystemVerilog provides different ways to copy objects and handles.

### Handle Assignment

Both handles refer to the **same object**.

```systemverilog
Packet pkt1;
Packet pkt2;

pkt1 = new();
pkt2 = pkt1;
```

```text
pkt1 ─────┐
          ├──> Same Object
pkt2 ─────┘
```

Changing the object through either handle affects the same object.

---

### Shallow Copy

A shallow copy creates a **new object**, but nested class handles continue to reference the same sub-objects.

```text
Object A ──> Sub-Object
Object B ──> Same Sub-Object
```

---

### Deep Copy

A deep copy creates a **completely independent object hierarchy**, including new copies of nested class objects.

```text
Object A ──> Sub-Object A

Object B ──> Sub-Object B
```

Deep copying generally requires a user-defined copy method.

---

## Downcasting

**Downcasting** converts a base-class handle into a derived-class handle.

SystemVerilog provides `$cast()` for runtime-checked casting.

```systemverilog
Parent p;
Child  c;

p = new Child();

if ($cast(c, p))
    $display("Downcast successful");
else
    $display("Downcast failed");
```

---

## OOP in Verification

SystemVerilog OOP is primarily important for **verification environments** rather than describing synthesizable hardware.

Classes can model transactions such as:

```text
Transaction
     │
     ├── Address
     ├── Data
     ├── Control
     └── Methods
```

These objects can then be generated, randomized, transmitted to a DUT, monitored, compared, and collected for coverage.

This class-based approach is the foundation of **UVM**.

---

## Applications

OOP concepts are widely used in:

* SystemVerilog Verification
* Class-Based Testbenches
* Transaction Modeling
* Constrained-Random Verification
* Functional Verification
* Verification Components
* UVM Testbenches
* Reusable Verification Environments

---

## Tools

The examples can be simulated using:

* QuestaSim / ModelSim
* EDA Playground
* Synopsys VCS
* Cadence Xcelium
* Xilinx Vivado
* Any SystemVerilog-compatible simulator

---

## Conclusion

SystemVerilog OOP provides the foundation for building **modular, reusable, scalable, and maintainable verification environments**. Understanding classes, objects, inheritance, encapsulation, polymorphism, abstraction, and object copying is essential for developing advanced **class-based testbenches and UVM environments**.

These concepts provide the foundation for the next stages of SystemVerilog verification, including **randomization, assertions, functional coverage, and UVM**.

---

⭐ If you find this repository useful, consider giving it a star.

