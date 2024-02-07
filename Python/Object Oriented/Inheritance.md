Inheritance allows us to define a class that inherits all the methods and properties from another class.

**Parent class** is the class being inherited from, also called base class.
**Child class** is the class that inherits from another class, also called derived class.

**Create a Parent class**
Create a class named `Person`, with `firstname` and `lastname` properties, and a `printname` method:

```python
class Person:  
  def __init__(self, fname, lname):  
    self.firstname = fname  
    self.lastname = lname  
  
  def printname(self):  
    print(self.firstname, self.lastname)  
  
#Use the Person class to create an object, and then execute the printname method:  
  
x = Person("John", "Doe")  
x.printname()
```

**Create a child class**
To create a class that inherits the functionality from another class, send the parent class as a parameter when creating the child class:

```python
class Student(Person):  
  pass
```

**Use the `pass` keyword when you do not want to add any other properties or methods to the class.**

**Super() Function**

Python also has a `super()` function that will make the child class inherit all the methods and properties from its parent:

```python
class Student(Person):  
  def __init__(self, fname, lname):  
    super().__init__(fname, lname)
```

By using the `super()` function, you do not have to use the name of the parent element, it will automatically inherit the methods and properties from its parent.

**Add Properties**

Add a property called `graduationyear` to the `Student` class:

```python
class Student(Person):  
  def __init__(self, fname, lname):  
    super().__init__(fname, lname)  
    self.graduationyear = 2019
```

In the example below, the year `2019` should be a variable, and passed into the `Student` class when creating student objects. To do so, add another parameter in the __init__() function:

Example: Add a `year` parameter, and pass the correct year when creating objects:

```python
class Student(Person):  
  def __init__(self, fname, lname, year):  
    super().__init__(fname, lname)  
    self.graduationyear = year  
  
x = Student("Mike", "Olsen", 2019)
```

## Add Methods

Example: Add a method called `welcome` to the `Student` class

```python
class Student(Person):  
  def __init__(self, fname, lname, year):  
    super().__init__(fname, lname)  
    self.graduationyear = year  
  
  def welcome(self):  
    print("Welcome", self.firstname, self.lastname, "to the class of", self.graduationyear)
```

Learn [[Resources#^e5f4d7 | OOP]]



