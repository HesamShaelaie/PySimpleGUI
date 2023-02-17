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
