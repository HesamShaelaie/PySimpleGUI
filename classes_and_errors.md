# Classes, objects, and inheritance

In object-oriented programming (OOP), a  **class**  is a blueprint for creating  **objects**  (a particular data structure), providing initial values for state (member variables or attributes), and implementations of behavior (member functions or methods). Several programming languages support OOP and Python is one of them, just like Java.

An  **instance**  is a specific object created from a particular class. Classes are used to create and manage new objects and support  **inheritance**—a key ingredient in OOP and a mechanism for reusing code.

This is an example of the class `Dog`. `bagel` and `brownie` are instances of `Dog`, or you can think of `Dog` as the template for many other `Dog` instances.

```python
class dog(object):  
  
    # function that initializes the object  
  def __init__(self, name, age, breed):  
        self.name = name  
        self.age = age  
        self.breed = breed  
  
    # function that returns the human age of the dog  
  def get_human_age(self):  
        if self.age <= 1:  
            return 15*self.age  
        elif self.age <= 2:  
            return 15+9*(self.age-1)  
        else:  
            return 24 + 5*(self.age - 2)  
  
  
bagel = dog("bagel", 2, "Golden retriever")  # Initiating the instance bagel  
brownie = dog("brownie", 4, "Poodle")  # Initiating the instance brownie
```
A class is a way of organizing information about a type of data so a programmer can reuse elements when making multiple instances of that data type.
## Class definition and initiation

To define a class, we simply write `class` followed by the desired name 
```python
class dog(object): 
```
It is usually followed by the constructor method that is denoted in Python as `__init__()`. This method is used to initialize the **attributes** in a class; in our example, we used  `name`, `age`, and `breed` as characteristics of dogs.  
As arguments, it takes `self` (`self` here refers to the object itself) followed by any arguments relevant to the definition of the object. When called, the constructor creates the new object, runs the code inside, and returns the new object. We set an attribute named `att` by giving `self.att` a given value as shown in the code below.
```python
   def __init__(self, name, age, breed): 
		self.name = name  
        self.age = age  
        self.breed = breed  
```
An **instance** is a specific object created from a particular class. To create instances of a class, call the class using the class name and pass in whatever arguments its `__init__()` method accepts—in this example, the `__init__()` method takes `name`, `age`, and `breed`.

```python
bagel = dog("bagel", 2, "Golden retriever")  # Initiating the instance bagel
```
## Instance variable vs Class variable

Instance variables are the **attributes** that we have defined earlier, their values are unique for each instance, and making any changes to one does not change the other. However, class variables are proper to the class that we define. Let's consider this example:
```python
class dog(object):
	scientific_name ='Canis lupus familiaris'
    ...

bagel = Dog("bagel", 2, "Golden retriever")

print(Dog.scientific_name) # returns Canis lupus familiaris
>>> Canis lupus familiaris
print(bagel.scientific_name) # returns Canis lupus familiaris 
>>> Canis lupus familiaris
```
We can see that it can be accessed either using `class.variable` or `instance.variable`. If we set `dog.scientific_name = 'cute wolves'`, it will change for all instances.
```python
dog.scientific_name = 'cute wolves'
print(bagel.scientific_name)  # After change
>>> cute wolves
print(brownie.scientific_name)
>>> cute wolves
```
## Class methods
Methods are functions defined inside the class and give us the ability to apply operations on that specific object. They're defined using the keyword `def` and take as an argument `self` as well as other useful arguments. It is called on an instance as `instance.method(argument1, argument2, ...)`. An example is the method `def get_human_age(self)` shown above.
```python
print(bagel.get_human_age())
>>> 24 
```

# Inheritance
Inheritance is one of the main uses of classes in OOP. Let's say I wanted to add a class `servicedog`, I want to be able to keep track of the number of hours worked during the current week as well as their main job. I will still need to include `name`, `age`, and `breed` since they are still **attributes** of a `dog`. To avoid redundancy and make use of implemented methods, our `servicedog` class can **inherit** from `dog`. `servicedog` is considered a **subclass** of `dog`, and `dog` is called a **superclass** of `servicedog`.

```python
class dog(object):
# Some code here

class servicedog(dog):
#Some code here
```
Inheritance allows code to be reused and reduces the complexity of a program. The derived classes (descendants) override or extend the functionality of base classes (ancestors).

When inheriting, the method `__init__` can be omitted if no change will happen in the initialization part since the constructor from the **superclass** would be used. In our example, we would like to add the attribute `currentjob` and `hoursworked`. The class will be written as 
``` python
class servicedog(dog):

	def __init__(self, name, age, breed, currentjob, hoursworked):
		super().__init__(name, age, breed)
		self.currentjob = currentjob
		self.hoursworked = hoursworked 
		
```
We can still use all methods from the class `dog` such as `get_human_age`.


#  Errors

Errors are problems in a program due to which the program will stop the execution. On the other hand, exceptions are raised when some internal events occur which change the normal flow of the program.  
Two types of Errors occur in python.  

1.  Syntax errors
2.  Logical errors (Exceptions)

An example of a syntax error is the following:
```python
print "Happy Friday!"
>>> SyntaxError: Missing parentheses in call to 'print'. Did you mean print("Happy Friday!")?
```

Exceptions or logical errors are multiple, here is a table that summarizes the most common built-in exceptions. 

|Exception  | Description |
|--|--|
| ZeroDivisionError | When you divide by zero |
|IndexError|When the wrong index of a list is retrieved|
|AttributeError |It occurs when an attribute assignment is failed|
| ImportError | It occurs when an imported module is not found|
|KeyError | It occurs when the key of the dictionary is not found|
|NameError|It occurs when the variable is not defined|
|MemoryError|It occurs when a program runs out of memory
|TypeError | It occurs when a function and operation are applied in an incorrect type

## Error Handling

When we are not sure if a line or lines of code can raise an error, we wrap them in a `try: ... except:` statement. It is similar to `try ... catch` that you might be familiar with from Java. Here is an example. 
```python
number_of_users = 0
amount_of_books = 1000
try:
     # print the ratio books:users
     print(amount_of_books/number_of_users)
# if an error occurs then it goes in except block
except:
     print("an error occurs")
print("End of code")
```
The code will return
```python
>>> an error occurs
>>> End of code
```
When an exception occurs in the block `try` occurs, the block `except` is executed. 
A specific type of exception can be specified in front of the `except` keyword. The subsequent block will be executed only if the specified exception occurs. There may be multiple `except` clauses with different exception types in a single try block. 
```python
a=5
b=0
try:
    print (a/b)
except TypeError:
    print('Unsupported operation')
except ZeroDivisionError:
    print ('Division by zero not allowed')
```


The error handling can be extended to include `else` and `finally` statements.
```python
try:
    #statements in try block
except:
    #executed when error in try block
else:
    #executed if try block is error-free
finally:
    #executed irrespective of exception occurred or not
```
The block else will only be executed if no error was raised whereas the block `finally` will always be executed at the end, even if one of the blocks contains a `return` statement.  

## Raising exceptions

Python also provides the  `raise`  keyword to be used in the context of exception handling. It causes an exception to be generated explicitly. Built-in errors are raised implicitly. However, a built-in or custom exception can be forced during execution.

The following code accepts a number from the user. The try block raises a ValueError exception if the number is outside the allowed range.

```python
try:
    x=int(input('Enter a number upto 100: '))
    if x > 100:
        raise ValueError(x)
except ValueError:
    print(x, "is out of allowed range")
else:
    print(x, "is within the allowed range")
```
