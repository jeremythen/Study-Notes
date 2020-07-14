

# Important

Check the doc for the built-in functions

---


Comment

```python
# This is a comment
```

If indentation is not right, a 'IndentationError: unexpected indent' error will show up.

* Checking the type of a variable

```python
type(num) # python 2 <type 'int'>, python 3 <class 'int'>
```

# Types

<class 'str'>
<class 'int'>
<class 'bool'>
<class 'float'>
<class 'int'>

## Parsing types:

```python
str(5)      # "5"
int("10")   # 10
float("10") # 10.0
float(10)   # 10.0
```


# Notes

Using true instead of True will throw an error: 'NameError: name 'true' is not defined'

There is no difference between '' and "" in python.

```python

# Multiline string:

"""Doc string
    multi line"""

```
## Showing the list of keywords

```python
import keyword
keyword.kwlist
```

# Operators

## Arithmetic

* //  Floor division  x // y
* **  Exponentiation  x ** y
* %   modulus


## Logical

* and
* or
* not

## Identity

* is        x is y
* is not    x is not y


```python
x = ["apple", "banana"]
y = ["apple", "banana"]
z = x

print(x is z)

# returns True because z is the same object as x

print(x is y)

# returns False because x is not the same object as y, even if they have the same content

print(x == y)

# to demonstrate the difference betweeen "is" and "==": this comparison returns True because x is equal to y

```

## Membership

* in        x in y
* not in    x not in y


```python
fruits = ["apple", "banana"]
print("banana" in fruits)
print("banana" not in fruits)
```

# Conditional

```python
is_available = True

if is not is_available:
    print("It is available")


data = None

if data:
    print("Has data")
else:
    print("No data")

# Inline

if num_a > num_b: print("num_a is greater than num_b")

print("Number is five") if num_a > 5 else print("Number is not 5") # Valid

if num > 5 and num < 15: # or
    print("num " + num)


```

# Loops

```python
for i in range(5):
    print(i) # 0 1 2 3 4

for i in range(5):
    print(i) # 1 2 3 4


```

# Pass and Continue in a loop

```python
for i in range(1, 10):
    if i == 3:
        pass # or continue
    elif i == 6:
        break   # Loops exits after reading this
    else:
        print(i)
```

# Adding an else to a while loop

```python
i = 0

while i < 5:
    print("Number", i)
    i += 1
else:
    print("Number is greater than 4 now")


```

# print() used a console.log()

```python
print("First argument", "Second", "Third") # First argument Second Third
```


# Dictionary

```python
dic = {"name": "Jeremy"}

name = "jeremy"

dic = { name: "Jeremy" }

print(dic)

print(dic.get("name")) ## Used also to get values

# If a key that doesn't exit is requested like dic["key"] it fails. With .get("key") it returns None.


# Checking if a key exists:

if "age" in dic.keys():
    print("age is a key")

```

Checking if a dictionary is empty:

```python
if dic:
    print("Is not empty")
# or
isEmpty = bool(dic)
# or
isEmpty = dic == {}

```
Removing a key-value pair:

```python
dic.pop("age")

# or

del dic["age"]
```

Copy a dictionary:

dictB = dictA.cody()



# Lists


```python

list = [1,2,3,4,5,6,7]

# Getting a range of the list:

list[2:5]

# Adding items

list.append(8)

# Removing an element from the list:

list.remove("item") # The value of the item. Only deletes the first occurrence.

# Checking if a value is in the list:

isInList = 3 in list

# Copy the list:

list2 = list.copy()

# Check the length of the list:

len(list)

# Joining 2 lists:

list3 = list1 + list2

# Accessing an invalid index throws IndexError

```

# Tuples

tuple = (1,2,3,4,5)

All other operations are same as list, except that tuples are immutable.

Converting a tuple to a list and vice versa.
```python
>>> data = ( 1, 3 , 5, "bye")
>>> data_two = list(data) # Convert data to list
>>> data_two[1] = 8 # Update value as list is mutable
>>> data = tuple(data_two) # Convert again to tuple
>>> data
(1, 8, 5, 'bye')
```

# Sets

aSet = {"hello", 25, 15, "etc"}

As sets are unindexed we cannot directly access the value in a set. Thus to access the value in the set you need to use a for loop.

>>> for i in data:
...     print(i)

You cannot change a value once the set is created.

Adding a value:

mySet.add('new value')

```python
# Other methods

mySet.remove('item')
len(mySet)

```

# Functions

Calling a function without () returns it's reference like: <function hello_world at 0x1083eb510>

Python has High Order Functions

If calling the function without the required arguments:
TypeError: add() missing 2 required positional arguments: 'a' and 'b'

If called with more arguments:
TypeError: add() takes 2 positional arguments but 3 were given

Python has named parameters (Keyword Arguments):

myFunc(a = 5)


## Args

Varargs are defined in python like:

```python

def add(*num): # where num, now is a tuple of args
    print(num)
    print(sum(num))

```

Default arguments

```python
# Just like in Javascript

def my(a, b = 5) # but now you can call the function without that argument, otherwise, calling it without it would fail.


def my(a = 3, b) # This is not legal in python. SyntaxError: non-default argument follows default argument

# Remember: All compulsory arguments must be declared first and then the default argument must be declared.

```

## Kwargs

With kwargs (**) you receive a dic as a parameter containing the named parameters (keyword arguments):

```python
def user(**username):
    print(username)     # {}

user(name = "Jeremy", age = 26) # {'name': 'Jeremy', 'age': 26}


```

# Keywords

## None

None is not False or 0 or []

Functions without a return statement (void) will return None.

## as, import, from

Used to create an alias while importing a module:

```python
import math as myAlias

# Importing a function from a module
from math import cos


```
There are two ways to import from a directory.

Method 1: from data import hello
Method 2: import data.hello

Where data is a module, a directory where a file named hello.py is.

Well python by default does not treat a directory as a module. To inform Python to treat a directory as a module, __init__.py is required.


```python

from data import hello
from data.info import info # Where info is a folder inside data folder, both with a __init__.py file in them.

hello.say_hello()

info.get_info()

```

## assert

Same as Java.
Throws AssertionError

## del

Deletes a reference to an object, variable, an item from a list or dictionary, etc.

```python
a = b = 5
del a
>>> a # Error

a = ['x', 'y', 'z']
del a[1]
a # ['x', 'z']
```

## try except finally raise

```python
try:
    a = 5 / 2
except:
    print("in except")
    # raise ZeroDivisionError('cannot device by zero')
finally:
    print("in finally")
```


## global

Used to modify a global variable, a variable declared outside of a function, if a function wants to edit it,
then it will need to declare it global inside.

```python
globvar = 10
def read1():
    print(globvar)
def write1():
    global globvar
    globvar = 5         # modifies the variable
def write2():
    globvar = 15        # does not modify the variable, since didn't specify global on it.
```

## in

```python
a = [1,2,3,4,5]
print(5 in a) # True

for i in 'hello':
    print(i)
```

## is


```python
>>> True is True
True
>>> False is False
True
>>> None is None
True

>>> [] == []
True
>>> [] is []
False
>>> {} == {}
True
>>> {} is {}
False

>>> '' == ''
True
>>> '' is ''
True
>>> () == ()
True
>>> () is ()
True

Unlike list and dictionary, string and tuple are immutable (value cannot be altered once defined). Hence, two equal string or tuple are identical as well. They refer to the same memory location.

```

## lambda

```python
a = lambda x: x * 2
for i in range(1, 6):
    print(a(i))


mySum = lambda a, b, c: a + b + c

mySum(1, 2, 3)
    
```

## nonlocal

Used to specify that a variable inside a nested function belongs to the outer function, so the inner function
doesn't create it.

```python
def outer_function():
    a = 5
    def inner_function():
        nonlocal a
        a = 10
        print("Inner function: ",a)
    inner_function()
    print("Outer function: ",a)

outer_function()
```

## with

with statement is used to wrap the execution of a block of code within methods defined by the context manager.
Use it just like Java Try With Resources.

```python
with open('example.txt', 'w') as my_file:
    my_file.write('Hello world!')
```

## yield

Used to create generators

```python

g = (2**x for x in range(100)) # A type of generator
next(g)     # 1
next(g)     # 2

def generator():    # another type of generator
    for i in range(6):
        yield i * I

g = generator()

for i in g:
    print(i) # 0 1 4 etc

```

# List comprehension

Is a way to create a list from another list or iterable for.

```python
letters = [ letter for letter in 'human' ]

letters = list( letter for letter in 'human' )

numbers = [ i * 2 for i in range(5) ]

numbers = [ i * 2 for i in range(5) ]

squares = list(map(lambda x: x ** 2, range(10)))

num_list = list((i, j) for i in range(10) for j in range(10) if i == j) # [(0, 0), (1, 1), (2, 2), (3, 3), (4, 4), (5, 5), (6, 6), (7, 7), (8, 8), (9, 9)]


```

# Dict comprehension

```python

tempDict = {t: (t * 9/5 ) + 32 for t in temps if t < 100}

dict1 = {"Jeremy": 20, "Juan": 21 }
dict2 = {"Maria": 10, "Jack": 26 }

newDict = {k: v for team in (dict1, dict2) for k,v in team.items()} # {'Jeremy': 20, 'Juan': 21, 'Maria': 10, 'Jack': 26}


```

# Sets comprehension

The same as list comprehension but with {}

letters = {letter for letter in 'human'}


# OOP

In a class, all methods needs to take the self argument, otherwise it will not work, since it's required.


# Special variables and methods

* __name__      The name of a module
* __doc__       The docstring of a class or function:
  
```python
class Car:
    "This is the doc of this class"

Car.__doc__

```

* ___getattr__(self, name)      Gets called when a property that doesn't exists in an object is requested.
* getattr                       Used to get a property from an object like getattr(object, 'property')

```python
class ATest:
    
    class_wide_var=0
    
    def __init__(self):
        self.x=5
        self.y=7
        self.z=10
        ATest.class_wide_var+=1
     
    def add(self,num1,num2):
        return num1+num2
        
    def __getattr__(self,name):
        print("Not Found")


a=ATest()
#x=a.novar

getattr(a, 'x')


# Setting values

class ATest:
    
    class_wide_var=0
    
    def __init__(self):
        self.x=5
        self.y=7
        self.z=10
        ATest.class_wide_var+=1
     
    def add(self,num1,num2):
        return num1+num2
        
    def __getattr__(self,name):
        print("Not Found")
        
    def __setattr__(self, name, value):
        ## setattr(ATest._instance, name, value) # This is failing, find out how to do it.
        print("Setting attr %s =  %s" %(name, value))
        


a=ATest()
#x=a.novar

setattr(a, 'x', 70)

getattr(a, 'x')

```

## Inheritance

```python
class Vehicle:
 
    def __init__(self, brand_name, color):
        self.brand_name = brand_name
        self.color = color
 
    def get_brand_name(self):
        return self.brand_name
 
class Car(Vehicle):
 
    def __init__(self, brand_name, model, color):  
        super().__init__(brand_name, color)         # super() returns a temp reference to the parent object and we call the method __init__ directly. 
        self.model = model
 
    def get_description(self):
        return "Car Name: " + self.get_brand_name() + self.model + " Color:" + self.color
 
c = Car("Audi ",  "r8", " Red")
print("Car description:", c.get_description())
print("Brand name:", c.get_brand_name())

```

## Multiple Inheritance

```python

class Vehicle:

    def __init__(self, brand_name):
        self.brand_name = brand_name
    
    def get_brand_name(self):
        return self.brand_name


class Cost:		

    def __init__(self, cost):
        self.cost = cost
    
    def get_cost(self):
        return self.cost

 
class Car(Vehicle, Cost):	

    def __init__(self, brand_name, model, cost): 
        self.model = model 
        Vehicle.__init__(self, brand_name)          # Calling the parents this way and passing self
        Cost.__init__(self, cost) 

    def get_description(self):
        return self.get_brand_name() + self.model + " is the car " + "and it's cost is " + self.get_cost()
		
c = Car("Audi ",  "r8", "2 cr")
print("Car description:", c.get_description())


```

## Encapsulation

With __prop that prop is private.
If you try to access it outside of the class a "AttributeError: 'Car' object has no attribute '__engine'" is thrown.

__engine(self) is now a private method.

This is a way to access a private property:

```python
c = Car()
print(c.get_description())
print("Accessing Private Method: ", c._Car__engine()) 
print("Accessing Private variable: ", c._Car__engine_name)
```


# Decorators

```python

# Method 1

def my_dec(func):
    def wrapper():
        print("first line")
        func()
        print("second line")
    return wrapper

def say_hello():
    print("Hello I am line Number 2")

print(my_dec(say_hello))

# Method 2

def my_dec(func):
    def wrapper():
        print("first line")
        func()
        print("second line")
    return wrapper

@my_dec
def hello():
    print("middle line")
    
    
hello()
```

# JSON Handling


```python

import json

json_string = '{ "user_name":"Sharvin", "age":1000}' #JSON String

# From string to dictionary, like JSON.parse() in Javascript
data = json.loads(json_string)

type(data) # <class 'dict'>

# From dictionary to JSON string, like JSON.stringify()
jsonString = json.dumps(data)

type(jsonString) # <class 'str'>


```


--------------------------------------- LinkedIn Learning


```python

# Strings and bytes are not the same thing in python

b = bytes([0x41, 0x42])


bDecoded = b.decode('utf-8') # This turns the bytes into string.

s = "String"

stringToBytes = s.encode('utf-8') # This turns a string into bytes


##################


```

# String format

```python

    "My name is {0} and I'm {1} years old".format("Jeremy", 26)

```


# Template String


```python

from string import Template

template = Template("My name is ${name} and I'm ${age} years old")

str = template.substitute(name="Jeremy", age=26) # or with a dictionary


```


# Built-in functions


iter

```python

myIterator = iter([1,2,3,4])

myNext = next(myIterator)


# Or

with open("myfile", 'e') as myFile:
    for line in iter(myFile.readLine, ''): # '' is the sentinel value, the iter will stop when it reads it.
        print(line)

```

enumerate

```python

for i,value in enumerate([10, 11, 12, 13, 14], start=1): # value will have the value of the list, and i will have the 'start' value.
    print(i, m)


```

zip

Is useful to combine multiple iteratable objects, returns a single iterable with a tuple on each record containing the records of all the iterables at that index.

```python

for m in zip([1,2,3,4,5], [5,4,3,2,1], [5,3,1,4,2]):
    print(m) # (1,5,5), (2,4,3), (3,3,1)


for 1,m in enumerate(zip([1,2,3,4,5], [5,4,3,2,1], [5,3,1,4,2]), start=1):
    print(i, m) # (1,5,5), (2,4,3), (3,3,1)


```

filter


```python

filteredArray = list(filter(predicateFunction, array))

data = [1,2,3,4,5]
filteredTata = list(filter(lambda x: x % 2 == 0, data)) # [2, 4]


chars = ['J', 'e', 'r', 'e', 'm', 'y']
filteredTata = list(filter(lambda x: x.isupper(), chars)) # ['J']


```

map

```python

data = [1,2,3]
filteredData = list(map(lambda x: x * x, data)) # [1, 4, 9]

```

sorted

```python

sortedData = sorted([4,2,5,7,1]) # Returns a new list, sorted.


```

# Itertools


```python

# cycle

import itertools

cycle1 = itertools.cicle([1,2,3])

print(next(cycle1)) # 1
print(next(cycle1)) # 2
print(next(cycle1)) # 3
print(next(cycle1)) # 1
print(next(cycle1)) # 2

# count

count = itertools.count(startValue, stepValue)

count = itertools.count(100, 10)

print(next(count)) # 100
print(next(count)) # 110
print(next(count)) # 120


# accumulate

data = [10, 15, 20, 25, 30, 4, 10, 80, 3, 14]

value = itertools.accumulate(data) # I defaults to sum, it will sum all of those values. Or pass a function to tell it when to stop and return that max:


value = itertools.accumulate(data, max) # The built-in max function. This will return 30 and accumulate will sum the numbers until they reach that number and will return that.

print(list(value)) # [10, 15, 20, 25, 30, 30, 30, 80, 80, 80]


# chain

data1 = ['1','2','3']
data2 = ['a', 'b', 'c']

data = itertools.chain(data1, data2)

print(list(data)) # ['1','2','3', 'a', 'b', 'c']


# dropwhile, this will drop values from a iterable until a condition is met.\


data = [1,2,3,4,5,6]

print(list(itertools.dropwhile(lambda x: x < 4, data))) # [4, 5, 6]. In this case, if < was >, then it would stop right away without dropping anything because the condition returns false staring.


# takewhile, this will allow items that meet the condition

print(list(itertools.takewhile(lambda x: x < 4, data))) # [1,2,3]. In this case, if < was >, then it would not take anything and return an empty [], since the condition returns false starting.

```

# Advanced Collections

```python
import collections

# Named tuples

named = collections.namedtuple("MyTuple", "a b c")
myTuple = named(a = "myA", b = "myB", c = "myC")

print(myTuple) # MyTuple(a='myA', b='myB', c='myC')

print(myTuple.a) # myA


# defaultdict. If you try to access a key that doesn't exist in this collection, it will create that key and assign and return a default value specified.


my_dict = defaultdict(lambda: 10)

key_list = ['a', 'b', 'c']

for k in key_list:
    my_dict[k]  # {'a': 10, 'b': 10, 'c': 10}
    
print(my_dict)


# Counter

from collections import Counter

data1 = [1,2,3,4,5,3,4,2,4,5,5]
data2 = [6,7,8,9,0,7,6,8,6,3,1,4,4,2,6,5,7]

c1 = Counter(data1)
c2 = Counter(data2)

print(c1.values())

print(c2[7])


print(c1 & c2)
print(c1 | c2)

print(c1.most_common(3))

c1.update(c2) # Add the two counters

print(c1)
print(c2)


c1.subtract(c2)

print(c1)



# OrderedDict

from collections import OrderedDict # OrderedDict keeps the order of the original structure

data = [(1,2,3), (4,5,6)]
my_dic = {'a': 1, 'b': 2, 'c': 3}

my_order_dict = OrderedDict(data)

my_order_dict_from_dict = OrderedDict(my_dic)


my_order_dict.popitem(FALSE) # popitem receives a boolean indicating if it pops the last or first.


# deque

from collections import deque

data = [1,2,3,4,5]

my_deque = deque(data)


print(my_deque)     # deque([1, 2, 3, 4, 5])

my_deque.rotate(2)

print(my_deque)     # deque([4, 5, 1, 2, 3])

my_deque.rotate(-2)

print(my_deque)     # deque([1, 2, 3, 4, 5])

my_deque.pop()
my_deque.popleft()

my_deque.append(7)
my_deque.appendleft(8)



```


# Enum

```python

from enum import Enum

class MyEnum(Enum):
    APPLE = 1
    BANANA = 2
    ORANGE = 3
    TOMATO = 4

```


# __str__ and __repr__ functions

If your class overrideds the __repr__ function, it will be called whenever the 'toString' method would be called, but if you also override the __str__ method,
this will be called instead, and the __repr__ will only be called in the repr function like repr(object)


```python

class Person:
    __repr__(self):
        return "This is good for debugging purposes."
    
    __str__(self):
        return "This is good for human readable."


person = Person()

print(repr(person)) #  "This is good for debugging purposes."

print(str(person)) # "This is good for human readable."
print(person) # "This is good for human readable."
print("{0}".format(person)) # "This is good for human readable."

```

# __dir__ function

When overriding the __dir__function, and calling dir(object), it will print the properties of the object.


# Operator overloading

There is operator overloading in Python.

Just override one of the functions like:

* __add__
* __sub__
* __mul__
* __div__
* __floordiv__ # //
* __pow__
* __and__ # &
* __or__  # |

Also, the same, but with short hand:


* __iadd__ 
* __isub__
* __imul__
* __itruediv__
* __ifloordiv__ # //
* __ipow__
* __iand__ # &
* __ior__  # |

For comparison operators:

* __gt__    # o1 > o2
* __ge__    # o1 >= o2
* __It__    # o1 < 02
* __le__    # o1 <= 02
* __eq__    # o1 == o2
* __ne__    # o1 != 02


# Loggin


```python

import logging

logging.info("info")
logging.error("info")
logging.debug("info")
logging.warning("info")
logging.critical("info")


###

logging.basicConfig(level = logging.DEBUG, filename="output.log", filemode="w")



```