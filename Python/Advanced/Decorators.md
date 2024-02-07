Decorators are a special technique that allows a user to add new functionality to an existing object without modifying its structure.

What decorators basically does is that it wraps a function and provides additional functionality.

Simple use cases
1. It can be used to keep the logs 
2. can be used to time functions

Example:
**Timing a function**

The decorator function 
```python
import time

def timeIt(function):
    def wrapper(*args,**kwargs):
        start_time = time.time()
        function(*args,**kwargs)
        end_time = time.time()
        completion_time = end_time-start_time
        print(f"\nFunction: {function.__name__} | completed in: 
        {format(completion_time,'.4f')} sec \n")
    return wrapper
```

This function will now calculate the time it took to execute the `function` passed to it. The function is not actually passed as an argument but is written under the decorator function using '@'. 

```python
@timeIt
def hello(entity):
    print(f"Hello {entity}")


hello("nayan")
```

