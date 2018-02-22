# Object-Oriented Programming

## Principles
- Encapsulation: Implementation details of an object's method are hidden from users
- Abstraction: All but the relevant data and interface is hidden from users to reduce complexity and increase efficiency
- Inheritance: Code is reused by having classes inherit parent class(es)' functions and data members
- Polymorphism: Presenting the same interface for differing underlying forms (data types).  Polymorphism is demonstrated through method overloading (same function name, different input types). 

## Method Protection Levels
Public: Can be accessed from anywhere  
Protected: Can only be accessed by the current class and subclasses  
Private: Can only be accessed from within the class  

## Method Keywords
Static: Does not need to be run by an instance of a class  
Virtual: Expected to be redefined in all subclasses (ensures that the correct function is run).  Destructors should be virtual such that the correct one runs.  

## Abstract Classes Vs. Interfaces
- Interfaces cannot have data members but abstract classes can.
- Interfaces cannot have any implemented methods but abstract classes can.
- A class doesn't need to implement all the functions of its abstract parent but must implement all the functions in the interface