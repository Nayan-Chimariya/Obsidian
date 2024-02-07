Dunder or magic methods in `Python` are the methods having two prefix and suffix underscores in the method name. Dunder here means “Double Under (Underscores)”. These are commonly used for operator overloading. Few examples for magic methods are: `__init__, __add__, __len__, __repr__` etc.

The `__init__` method for initialization
```python
# declare our own string class
class String:
	
	# magic method to initiate object
	def __init__(self, string):
		self.string = string
		
# Driver Code
if __name__ == '__main__':
	
	# object creation
	string1 = String('Hello')

	# print object location
	print(string1)
```
**OUTPUT**
```python
<__main__.String object at 0x7fe992215390>
```

The above snippet of code prints only the memory address of the string object. Let’s add a `__repr__` method to represent our object.

```python
# declare our own string class
class String:
	
	# magic method to initiate object
	def __init__(self, string):
		self.string = string
		
	# print our string object
	def __repr__(self):
		return 'Object: {}'.format(self.string)

# Driver Code
if __name__ == '__main__':
	
	# object creation
	string1 = String('Hello')

	# print object location
	print(string1)
```
*OUTPUT*
```python
Object: Hello
```

**If we try to add a string to it :**

```python
# declare our own string class
class String:
	
	# magic method to initiate object
	def __init__(self, string):
		self.string = string
		
	# print our string object
	def __repr__(self):
		return 'Object: {}'.format(self.string)

# Driver Code
if __name__ == '__main__':
	
	# object creation
	string1 = String('Hello')
	
	# concatenate String object and a string
	print(string1 +' world')

```
**OUTPUT**
```python
**TypeError**: unsupported operand type(s) for +: 'String' and 'str'
```

Now add `__add__` method to String class :

```python
# declare our own string class
class String:
	
	# magic method to initiate object
	def __init__(self, string):
		self.string = string
		
	# print our string object
	def __repr__(self):
		return 'Object: {}'.format(self.string)
		
	def __add__(self, other):
		return self.string + other

# Driver Code
if __name__ == '__main__':
	
	# object creation
	string1 = String('Hello')
	
	# concatenate String object and a string
	print(string1 +' Geeks')
```
**OUTPUT**
```python
Hello Geeks
```

Learn [[Resources#^362e02 | Advance Python]]



