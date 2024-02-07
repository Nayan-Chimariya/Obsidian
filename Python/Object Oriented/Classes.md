## Introduction to class

Classes provide a means of bundling data and functionality together. Creating a new class creates a new _type_ of object, allowing new _instances_ of that type to be made. Each class instance can have attributes attached to it for maintaining its state. Class instances can also have methods (defined by its class) for modifying its state.


## Prerequisites
### Python Scopes and Namespaces

#### Namespaces
A namespace is a collection of currently defined symbolic names along with information about the object that each name references. You can think of a namespace as a `dictionary` in which the keys are the object names and the values are the objects themselves. Each key-value pair maps a name to its corresponding object.
1. Built-In
2. Global
3. Enclosing
4. Local

##### The Built-In Namespace

The **built-in namespace** contains the names of all of Python’s built-in objects. These are available at all times when Python is running. You can list the objects in the built-in namespace with the following command:

```python
dir (__builtin__)
``` 

##### The Global Namespace

The **global namespace** contains any names defined at the level of the main program. Python creates the global namespace when the main program body starts, and it remains in existence until the interpreter terminates.

This may not be the only global namespace that exists. The interpreter also creates a global namespace for any **module** that your program loads with the `import` statement. 

##### The Local and Enclosing Namespaces

The interpreter creates a new namespace whenever a function executes. That namespace is local to the function and remains in existence until the function terminates.

Functions don’t exist independently from one another only at the level of the main program. You can also define one function inside another:

```python
def f():
	print('Start f()')

    def g():
        print('Start g()')
        print('End g()')
        return

    g()

    print('End f()')
    return
    
f()
```

When the main program calls `f()`, Python creates a new namespace for `f()`. Similarly, when `f()` calls `g()`, `g()` gets its own separate namespace. The namespace created for `g()` is the **local namespace**, and the namespace created for `f()` is the **enclosing namespace**.


##### Searching namespace hierarchy 
1. **Local**: If you refer to `x` inside a function, then the interpreter first searches for it in the innermost scope that’s local to that function.
2. **Enclosing**: If `x` isn’t in the local scope but appears in a function that resides inside another function, then the interpreter searches in the enclosing function’s scope.
3. **Global**: If neither of the above searches is fruitful, then the interpreter looks in the global scope next.
4. **Built-in**: If it can’t find `x` anywhere else, then the interpreter tries the built-in scope.

![[LEGB Namespace.png]]






#### Scopes

Suppose you refer to the name `x` in your code, and `x` exists in several namespaces. How does Python know which one you mean?

The answer lies in the concept of **scope**. The scope of a name is the region of a program in which that name has meaning. The interpreter determines this at runtime based on where the name definition occurs and where in the code the name is referenced.

**Example 1: Single Definition**
In the first example, `x` is defined in only one location. It’s outside both `f()` and `g()`, so it resides in the global scope:

```python
1  >>> x = 'global'

2  >>> def f():
3  ...
4  ...     def g():
6  ...         print(x)
7  ...
8  ...     g()
9  ...
10  
11 >>> f()
12 global
```

The print() statement on line 6 can refer to only one possible `x`. It displays the `x` object defined in the global namespace, which is the string `'global'`.


**Example 2: Double Definition**
In the next example, the definition of `x` appears in two places, one outside `f()` and one inside `f()`
but outside `g()`:

```python
1 >>> x = 'global'

2  >>> def f():
3  ...     x = 'enclosing'
4  ...
5  ...     def g():
6  ...         print(x)
7  ...
8  ...     g()
9  ...

10 >>> f()
11 enclosing
```

As in the previous example, `g()` refers to `x`. But this time, it has two definitions to choose from:

- **Line 1** defines `x` in the global scope.
- **Line 4** defines `x` again in the enclosing scope.

According to the LEGB rule, the interpreter finds the value from the enclosing scope before looking in the global scope. So the `print()` statement on **line 7** displays `'enclosing'` instead of `'global'`.

**Example 3: Triple Definition**
Next is a situation in which `x` is defined here, there, and everywhere. One definition is outside `f()`, another one is inside `f()` but outside `g()`, and a third is inside `g()`:

```python
1  >>> x = 'global'

2  >>> def f():
3  ...     x = 'enclosing'
4  ...
5  ...     def g():
6  ...         x = 'local'
7  ...         print(x)
8  ...
9  ...     g()
10 ...

11 >>> f()
12 local
```

Now the `print()` statement on **line 8** has to distinguish between three different possibilities:

- **Line 1** defines `x` in the global scope.
- **Line 4** defines `x` again in the enclosing scope.
- **Line 7** defines `x` a third time in the scope that’s local to `g()`.

Here, the LEGB rule dictates that `g()` sees its own locally defined value of `x` first. So the `print()` statement displays `'local'`.

**Example 4: No Definition**
Last, we have a case in which `g()` tries to print the value of `x`, but `x` isn’t defined anywhere. That won’t work at all:

```python
1  >>> def f():
2  ...
3  ...     def g():
4  ...         print(x)
5  ...
6  ...     g()
7  ...
8
9  >>> f()
10 Traceback (most recent call last):
11   File "<stdin>", line 1, in <module>
12   File "<stdin>", line 6, in f
13   File "<stdin>", line 4, in g
14   NameError: name 'x' is not defined
```

This time, Python doesn’t find x in any of the namespaces, so the print() statement on line 4 generates a `NameError` exception.














## Class Syntax

```python
class ClassName:
    statement_1
    .
    .
    .
    statement_N
```

When a class definition is entered, a new namespace is created, and used as the local scope — thus, all assignments to local variables go into this new namespace. In particular, function definitions bind the name of the new function here.

When a class definition is left normally (via the end), a _class object_ is created. This is basically a wrapper around the contents of the namespace created by the class definition


## Class object

Class objects support two kinds of operations: attribute references and instantiation.
Valid attribute names are all the names that were in the class’s namespace when the class object was created. So, if the class definition looked like this:

```python
class MyClass:
    i = 12345

    def f(self):
        return 'hello world'
```

then `MyClass.i` and `MyClass.f` are valid attribute references, returning an integer and a function object, respectively.

Class _instantiation_ uses function notation. Just pretend that the class object is a parameterless function that returns a new instance of the class. For example (assuming the above class):

```python
x = MyClass()
```

creates a new _instance_ of the class and assigns this object to the local variable `x`.The instantiation
operation (“calling” a class object) creates an empty object

Many classes like to create objects with instances customized to a specific initial state. Therefore a class may define a special method named `__init__()`, like this:

```python
def __init__(self):
    self.data = []
```

The `__init__()` method may have arguments for greater flexibility. In that case, arguments given to the class instantiation operator are passed on to `__init__()`. For example,

```python
class Complex:
     def __init__(self, realpart, imagpart):
         self.r = realpart
         self.i = imagpart
         
>>> x = Complex(3.0, -4.5)
>>> x.r, x.i
(3.0, -4.5)
```

## Instance Objects

The only operations understood by instance objects are attribute references. There are two kinds of valid attribute names: data attributes and methods. For example, if `x` is the instance of `MyClass`created above, the following piece of code will print the value `16`, without leaving a trace:

```python
x.counter = 1
while x.counter < 10:
    x.counter = x.counter * 2
print(x.counter)
del x.counter
```










## Method Objects

Usually, a method is called right after it is bound:

```python
x.f()
```

In the `MyClass` example, this will return the string `'hello world'`. However, it is not necessary to call a method right away: `x.f` is a method object, and can be stored away and called at a later time. For example:

```python
xf = x.f
while True:
    print(xf())
```

## Classes and Instance Variables

Generally speaking, instance variables are for data unique to each instance and class variables are for attributes and methods shared by all instances of the class:

```python
class Dog:

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.kind                  # shared by all dogs
'canine'
>>> e.kind                  # shared by all dogs
'canine'
>>> d.name                  # unique to d
'Fido'
>>> e.name                  # unique to e
'Buddy'
```

shared data can have possibly surprising effects with involving [mutable](https://docs.python.org/3/glossary.html#term-mutable) objects such as lists and dictionaries. For example, the _tricks_ list in the following code should not be used as a class variable because just a single list would be shared by all _Dog_ instances:

```python
class Dog:

    tricks = []             # mistaken use of a class variable

    def __init__(self, name):
        self.name = name

    def add_trick(self, trick):
        self.tricks.append(trick)

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks                # unexpectedly shared by all dogs
['roll over', 'play dead']
```

Correct design of the class should use an instance variable instead:

```python
class Dog:

    def __init__(self, name):
        self.name = name
        self.tricks = []    # creates a new empty list for each dog

    def add_trick(self, trick):
        self.tricks.append(trick)

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks
['roll over']
>>> e.tricks
['play dead']
```

Go to [[Inheritance]]
Learn [[Resources#^e5f4d7 | OOP]]

