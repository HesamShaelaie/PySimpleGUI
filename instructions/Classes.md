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