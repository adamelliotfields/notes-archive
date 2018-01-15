# Python Notes

### Indentation
 - In Python, there are no curly braces to signify a code block.
 - Each line of code in the code block must be indented 4 spaces.

```python
im_a_parent:
    im_a_child:
        im_a_grandchild
    im_another_child:
        im_another_grand_child
```

### Comments
PEP257 guidelines encourage using double-quotes for Docstrings.

```python
""" This is a Docstring """
# This is a single-line comment
```

### Python Shell
 - Use the `exit()` function to exit the console or press `CTRL-D`.
 - Use the `KeyboardInterrupt` exception to return to the primary prompt by pressing `CTRL-C`.
 - When typing code that allows for continuation, pressing `ENTER` will give a new line.
 - Use `CTRL-J` to manually get a new line.
 - There is no `clear()` function in the Python console.

```python
""" delete all global variables """

for name in dir():
    if not name.startswith('_'):
        del globals()[name]
```

### Input
 - To ask the user for input, use the `input()` function.
 - `input()` was previously `raw_input()` in Python 2.x.

### Print
 - To print to the shell, use the `print()` function.
 - `print` was a statement in Python 2.x.

### Variables & Booleans
 - Simply declare your variable and assign its value.
 - Booleans are constants and are capitalized.

### Math
 - Additional math functions can be imported from the `math` module.
 - Note that in Python 2.x, division was strictly integer division unless the divisor was a float.

```python
2 + 2  # addition
2 - 2  # subtraction
2 * 2  # multiplication
2 / 2  # float division
2 // 2 # integer division
2 ** 3 # exponentiation
3 % 2  # modulo
```

### String Index
Each character in a string is assigned an index:

```python
+---+---+---+---+---+---+
| P | Y | T | H | O | N |
+---+---+---+---+---+---+
  0   1   2   3   4   5
```

### String Methods

```python
len()    # get the length of a string
.lower() # make a string lowercase
.upper() # make a string uppercase
str()    # convert a non-string to a string
```

### String Concatenation
 - A string and a non-string cannot be concatenated.
 - Non-strings must be converted to a string using the `str()` method.

```python
print("The value of pi is around " + str(3.14))
```

### String Substitution
When printing a variable with a string, use `%s`

```python
world = "World"
print("Hello %s" % world)
```

### `.format()`

```python
print("{} World").format("Hello")
```

### Date & Time
Import the datetime library.

```python
from datetime import datetime
now = datetime.now()
```

To print the date in American Numeric Notation, use string substitution:

```python
print('%s/%s/%s' % (now.month, now.day, now.year))
```

To print the time in 24-hour format:

```python
print('%s:%s:%s' % (now.hour, now.minute, now.second))
```

### Comparators

```python
=  # assigns a value to a variable
== # tests for equality, not identity

== # equal to
!= # not equal to
<  # less than
<= # less than or equal to
>  # greater than
>= # greater than or equal to
```

### Boolean Operators

```python
and # checks if both the statements are True (evaluated second)
or  # checks if at least one of the statements is True (evaluated third)
not # gives the opposite of the statement (evaluated first)
```

### Conditional Statements

```python
if 1 < 2:
    print(True)
else:
    print(False)
```

### Functions
 - Functions are defined with 3 components:
   - The header, which includes the def keyword
   - An optional comment explaining what the function does
   - The body, which describes the procedures the function carries out
 - Functions must be called in order to be implemented.
 - A function can also call another function in its body.

```python
def hello_world():
    print("Hello World!")

hello_world()
```

### Parameters and Arguments
 - A parameter acts as a variable name for a passed-in argument.
 - A list can be passed into functions.
 - A function can require as many parameters as you want, but you should pass in the required number of arguments when calling the function.

### Try and Except
 - `try` lets you "try" some code that could break (for example, with an incorrect user input).
 - The `except` block will run when the program encounters an error.
   - You can (and should) define an error type for `except` to catch (e.g., `ValueError`)

### Modules
 - A module is a Python object with attributes that you can bind and reference.
 - A module can define functions, classes, and variables.
 - A module can include runnable code.
 - Modules must be imported, but be careful with Universal Imports.

```python
""" Generic Import """
import math

# You have to tell the program that sqrt() comes from the math module
math.sqrt(4)

""" Function Import """
from math import sqrt

# When importing a specific function, you don't have to define the module
sqrt(4)

""" Universal Import """
from math import *

# When importing everything from a module, you also don't have to define it
sqrt(4)
```

### Built-in Functions

```python
max()  # takes any number of arguments and returns the largest
min()  # takes any number of arguments and returns the smallest
abs()  # returns the absolute value of a single integer
type() # returns the type of the data
```

### Lists
 - Lists are a datatype you can use to store a collection of different pieces of information.
 - You can access an individual list item by its index.
 - You can reassign a list item also using the item's index.

```python
array = [1, 2, 3, 4]

array[0] = "one"
```

You can add an item to the end of the list using the `append()` function.

```python
array = [1, 2, 3]

array.append(4)
```

You can add a list to the end of a list using the `extend()` function.

```python
array_1 = [1, 2]
array_2 = [3, 4]

array_1.extend(array_2)
```

You can also add lists together using `+`.

```python
array_1 = [1, 2]
array_2 = [3, 4]

return array_1 + array_2
```

You can add an item to a specific index using the `insert()` function (won't replace the existing item).

```python
array = [1, 2, 3, 4]

array.insert(4, 5)
```

You can remove an item using the `remove()` function.

```python
array = [1, 2, 3, 4]

array.remove(1)
```

You can remove an item at a given index using the `del` keyword.

```python
array = [1, 2, 3, 4]

del array[0]
```

You can return the index value of a specific item using the `index()` function.

```python
array = [1, 2, 3, 4]

array.index(1)
```

You can remove an item and return it (or store in a variable) using the `pop()` function.

```python
array = [1, 2, 3, 4]

num = array.pop(0)
```

You can sort a list using the `sorted()` function.

```python
array = [4, 3, 2, 1]

sorted(array)
```

You can get the length of a list using the `len()` function.

```python
array = [1, 2, 3, 4]

len(array)
```

### List Slicing
 - You can slice a list using slice notation.
 - Slices are EXCLUSIVE, meaning they stop at the last item, but don't return it.

```python
array[start:end]      # items start through end - 1
array[start:]         # items start through the rest of the list
array[:end]           # items from the beginning through end - 1
array[:]              # the whole list

array[start:end:step] # start through not past end, by step

array[-1]             # last item in the list
array[-2:]            # last two items in the list
array[:-2]            # everything except the last two items

array[::-1]           # the list in reverse

+---+---+---+---+---+---+
| P | Y | T | H | O | N |
+---+---+---+---+---+---+
  0   1   2   3   4   5
 -5  -4  -3  -2  -1  
```

You can also use the `slice()` function.

```python
In [1]: array = [1, 2, 3, 4]

In [2]: array[slice(1,3)]
Out[2]: [2, 3]
```

### For Loops
The variable after `for` takes on the value of each item in the list.

```python
numbers = [1,2,3,4]
for number in numbers:
    print number
```

You can nest for-loops to iterate through lists-of-lists.

```python
list_of_lists = [ [1, 2, 3], [4, 5, 6] ]

for i in list_of_lists:
    for item in i:
        print item
```

### The `in` Operator
 - Use the `in` operator to iterate over lists, tuples, dictionaries, and even strings.
 - The inverse of `in` is `not in` which can be used for comparison.

```python
for letter in "adam":
    if letter not in "aeiou":
        print letter
```

### Range
 - `range()` has up to 3 parameters: start, stop, step.
 - `range()` can be combined with the `list()` function to create a list.

```python
In [1]: list(range(5))
Out[1]: [0, 1, 2, 3, 4]

In [1]: list(range(1, 5))
Out[1]: [1, 2, 3, 4]

In [1]: list(range(1, 6, 2))
Out[1]: [1, 3, 5]
```

 - You can use `range()` in a for-loop to iterate.

```python
for i in range(len(array)):
    print array[i]
```

### List Comprehension Syntax
 - You can generate lists with specific criteria, like even numbers, multiples, squares, etc.

```python
In [1]: list(i for i in range(11) if i % 2 == 0)
Out[1]: [0, 2, 4, 6, 8, 10]

In [2]: list(i ** 3 for i in range(11) if (i ** 3) % 4 == 0)
Out[2]: [0, 8, 64, 216, 512, 1000]
```

### Enumerate
 - `enumerate()` is a built-in function that adds a counter to an iterable.
 - `enumerate()` starts counting at 0, but a second argument can be passed in to start counting at that number.
 - `enumerate()` returns an enumerate object, which is a sequence of tuples.

```python
In [1]: array = ["zero", "one", "two", "three"]

In [2]: for i, item in enumerate(array):
   ...:     print(i, item)
   ...:
0 zero
1 one
2 two
3 three
```

### Zip
 - `zip()` is a built-in function that creates pairs of elements when two (or more) lists are passed as arguments.
 - `zip()` will stop at the end of the shortest list.

```python
list_a = [1, 2, 3, 4, 5]
list_b = [2, 3, 2, 5, 4]

for a, b in zip(list_a, list_b):
    if a > b:
        print a
    else:
        print b
```

### For Else Loops
 - The `else` block will execute when the for loop ends normally.
 - If the for loop ends by a break statement, the else block will not run.

```python
for i in range(5):
    print(i)
else:
    print("Complete")
```

### While Loops
 - The while loop executes the code inside it as long as the condition is true.
 - Instead of executing something *if* it is true, the while executes something *while* it is true.
 - Make sure you incorporate some way for the condition to evaluate to false to avoid infinite loops.

```python
count = 0

while count <= 5:
    print(str(count))
    count += 1
```

You can also add an `if` statement with a break to exit the loop.

```python
count = 0

while True:
    print count
    count += 1
    if count >= 10:
        break
```

### Break vs Continue
 - The break statement provides you with the opportunity to exit out of a loop when an external condition is triggered.
 - The continue statement gives you the option to skip over the part of a loop where an external condition is triggered, but to go on to complete the rest of the loop.

```python
number = 0
for number in range (4):
    number += 1
    if number == 3:
        break
    print('Number is ' + str(number))

# Number is 1
# Number is 2
```

```python
number = 0
for number in range (4):
    number += 1
    if number == 3:
        continue
    print('Number is ' + str(number))

# Number is 1
# Number is 2
# Number is 4
```

### While Else Loops
 - The `else` block will execute when the `while` loop condition evaluates to `false`. 
 - The `else` block will execute even if the `while` loop is `false`.
 - If the `while` loop exits as the result of a `break`, the `else` block will not be executed.

### Dictionaries
 - Dictionaries are similar to PHP Associative Arrays.
 - Dictionaries are enclosed in curly-braces, are key-value pairs, and are separated by commas.
 - You can add new key-value pairs to the dictionary using bracket notation.
 - You can add or update key-value pairs using the `.update()` method.
 - You can remove key-value pairs with the `del` keyword.

```python
In [1]: dictionary = {
   ...: "key_1" : 1,
   ...: "key_2" : 2,
   ...: "key_3" : 3
}

In [2]: dictionary["key_4"] = 4

In [3]: dictionary["key_4"]
Out[3]: 4
```

### Looping Over a Dictionary
 - When used on a dictionary, the variable after `for` is the key.
 - Remember to use bracket notation to access the value of they key.

```python
dictionary = {
    "key_1" : 1,
    "key_2" : 2,
    "key_3" : 3,
    "key_4" : 4
}

for key in dictionary:
    print(dictionary[key])
```

### Dictionary Functions
 - You can access the key-value pairs of a dictionary using the `items()` function.
 - `items()` returns a list of tuples of key-value pairs.

```python
In [1]: dictionary = {
   ...: "key_1" : 1,
   ...: "key_2" : 2,
   ...: "key_3" : 3,
   ...: "key_4" : 4
}

In [2]: dictionary.items()
Out[2]: dict_items([('key_1', 1), ('key_2', 2), ('key_3', 3), ('key_4', 4)])
```

You can access the keys using the `keys()` method.

```python
In [1]: dictionary = {
   ...: "key_1" : 1,
   ...: "key_2" : 2,
   ...: "key_3" : 3,
   ...: "key_4" : 4
}

In [2]: dictionary.keys()
Out[2]: dict_keys(['key_1', 'key_2', 'key_3', 'key_4'])
```

You can access the values using the `values()` method.

```python
In [1]: dictionary = {
   ...: "key_1" : 1,
   ...: "key_2" : 2,
   ...: "key_3" : 3,
   ...: "key_4" : 4
}

In [2]: dictionary.values()
Out[2]: dict_keys([1, 2, 3, 4])
```

### Dictionary Packing
Putting multiple keyword arguments into a single dictionary.

```python
In [1]: def packer(**kwargs):
   ...:     print(kwargs)

In [2]: packer(first="Adam", last="Fields")
Out[2]: {'first': 'adam', 'last': 'fields'}
```

### Dictionary Unpacking
Pulling multiple keys-value pairs out of a dictionary to feed them to a function.

```python
In [1]: def unpacker(first=None, last=None):
   ...:     if first and last:
   ...:         print("Hi {} {}!").format(first, last)
   ...:     else:
   ...:         print("Hi no name!")
 
In [2]: unpacker(**{"first", "adam", "last": "fields"})
Out[2]: Hi adam fields!
```

### Tuples
 - Tuples are like lists in that each member has an index, can be looped over, and each item can be any data type.
 - Unlike lists, tuples are immutable (cannot be changed).
 - If an item in the tuple is mutable (like a list), you can modify it (but not remove it).

```python
my_tuple = (1, 2, 3)
```

### Sets
 - A set contains an unordered collection of unique and immutable objects.
 - Sets cannot have multiple occurences of the same item. 
 - You can add an item to a set using the `.add()` method. 
 - You can remove an item using `.remove()`.
 - You can also add items from other sets using the `.update()` method. 
 - Because sets are unnorderd, they do not support indexing or slicing.

```python
my_set = {1, 2, 3}
```

### Set Operations
 - `|` or `.union(*others)` returns all of the items from all of the sets.
 - `&` or `.intersection(*others)` returns all of the common items between all of the sets.
 - `-` or `.difference(*others)` returns all of the items in the first set that are not in the other sets.
 - `^` or `.symmetric_difference(other)` returns all of the items that are not shared by the two sets.

### Lambdas
 - Lambdas are anonymous functions (they don't need a name).
 - Lambdas are useful for when you need a quick function.
 - If you plan on reusing a function, you're better off defining it.

```python
In [1]: def f(x):
   ...:     return x ** 2

In [2]: f(2)
Out[2]: 4

In [1]: g = lambda x: x ** 2

In [2]: g(2)
Out[2]: 4
```

### The Base 2 Number System
 - When we count, we do it in base 10 (0-9).
 - In binary, we count in base 2 (0 or 1).

```python
0b0    # 0
0b1    # 1
0b10   # 2
0b11   # 3
0b100  # 4
0b101  # 5
0b110  # 6
0b111  # 7
0b1000 # 8
0b1001 # 9
0b1010 # 10
0b1011 # 11
0b1100 # 12
0b1101 # 13
0b1110 # 14
0b1111 # 15
```

### Converting Integers to Binary
The `bin()` function takes an integer as input and returns the binary representation as a string.

```python
In [1]: bin(42)
Out[1]: '0b101010'
```

You can convert binary numbers to integers using the `int()` function and passing in 2 arguments: the binary number (as a string) its base (2).

```python
In [1]: int('101010', 2)
Out[1]: 42
```

### Bitwise Operations
Bitwise operations directly manipulate bits.

```python
>>  # Right Shift
<<  # Left Shift
&   # Bitwise AND
|   # Bitwise OR
^   # Bitwise XOR
~   # Bitwise NOT
```

Shifting is the equivalent of dividing (right shift) or multiplying (left shift) by 2.
 - Shifting by 2 would be equivalent of multiplying/dividing by 4 (2 ** 2).

```python
In [1]: 16 >> 1
Out[1]: 8

In [1]: 8 << 1
Out[1]: 16
```

The bitwise `&` (AND) operator compares 2 numbers and returns a number where the bits are turned on if the corresponding bits of both numbers are 1.

```python
In [1]: bin(0b1110 & 0b101)
Out[1]: '0b100'
```

The bitwise `|` (OR) operator compares 2 numbers and returns a number where the bits are turned on if either of the corresponding bits of both numbers are 1.

```python
In [1]: bin(0b1110 | 0b101)
Out[1]: '0b1111'
```

The bitwise `^` (XOR) operator compares 2 numbers and returns a number where the bits are turned on if either of the corresponding bits of both numbers are 1 (but not both).

```python
In [1]: bin(0b1110 ^ 0b101)
Out[1]: '0b1011'
```

The bitwise `~` (NOT) operator flips the bits of a single number. 
 - Mathematically, this is equivalent to adding 1 to the number and making it negative.

```python
In [1]: ~10
Out[1]: -11

In [1]: ~0b1010
Out[1]: -11
```

### Bit Mask
A bit mask is a variable that aids you with bitwise operations.
 - A bit mask can help you turn specific bits on or off, or collect data from an integer about which bits are on or off.

```python
# create a variable containing the number 12 (0b1100)
num = 0b1100

# create a variable with the 3rd bit on
mask = 0b0100

# check to see if the 3rd bit from the right of num is on
if num & mask > 0:
    print True
```

You can use masks to turn a bit in a number on using `|` (OR).
 - `|` will turn a corresponding bit on if it's off and leave it on if it's already on.

```python
In [1]: num = 0b10111011

In [2]: mask = 0b100

In [3]: bin(num | mask)
Out[3]: '0b10111111'
```

You can use masks to flip a bit in a number using `^` (XOR).

```python
In [1]: num = 0b11101110

In [2]: mask = 0b11111111

In [3]: bin(num | mask)
Out[3]: '0b10001'
```

You can use the shift operators to slide masks into place.

```python
# define a function with 2 parameters
def flip(num, n):
    # create a mask that shifts n - 1 places to the left
    mask = 0b1 << n - 1
    # flip the bit using XOR
    result = num ^ mask
    return bin(result)
```

### Object Oriented Python
 - Python is an object oriented programming language which means it manipulates programming constructs called objects.
 - Objects are data structures that contain data (properties) and functions (methods).
 - For example, a string is an instance of the `str` class and a dictionary is an instance of the `dict` class.

### Classes
 - A basic class consists only of the `class` keyword, the name of the class, and the class from which the new class inherits from.
 - The `__init__()` method is required for classes and always takes at least one argument, `self`.
 - Python will use the first parameter that `__init__()` receives to refer to the object being created.
 - You can use the `pass` keyword as a placeholder in the class body.
 - The `__repr__()` method is used to define how the object is represented when printed. 

```python
class ShoppingCart(object):
    ''' Creates shopping cart objects '''
    items_in_cart = {}
    def __init__(self, customer_name):
        self.customer_name = customer_name

    def add_item(self, product, price):
        ''' Add product to the cart '''
        if not product in self.items_in_cart:
            self.items_in_cart[product] = price
            print product + " added."
        else:
            print product + " is already in the cart."

    def remove_item(self, product):
        ''' Remove product from the cart '''
        if product in self.items_in_cart:
            del self.items_in_cart[product]
            print product + " removed."
        else:
            print product + " is not in the cart."
```

### Class Scope
 - **Global Variables:** Variables that are availably anywhere.
 - **Member Variables:** Variables that are only available to members of certain classes.
 - **Instance Variables:** Variables that are only available to particular instances of a class.

### Inheritance

 - Classes can inherit properties and methods from their parent class.
 - Parent classes can also be called superclasses and child classes can also be called subclasses.
 - A subclass can also override its inherited attributes.
 - You can directly access the attributes or methods of a superclass with the `super()` function.

```python
class Employee(object):
    def __init__(self, employee_name):
        self.employee_name = employee_name
    def wage(self, hours):
        self.hours = hours
        return hours * 20.00

class PartTimeEmployee(Employee):
    def part_time_wage(self, hours):
        self.hours = hours
        return hours * 15.00
    def full_time_wage(self, hours):
        return super(PartTimeEmployee, self).wage(hours)
```

### File Input/Output
 - The `open()` function takes 2 arguments:
   - The first argument is a string containing the file.
   - The second argument is another string containing the mode:
     - `"r"` when the file will only be read
     - `"w"` when the file will be written to (any existing data will be erased)
     - `"a"` appends any new data to the file.
     - `"r+"` opens the file for both reading and writing
   - If no second argument is given, Python uses the `"r"` mode by default.
 - The `write()` function takes a string as an argument (the data to be written).
 - The `read()` function allows you to read data from the file.
 - The `readline()` function allows you to read data line-by-line.
 - You must use the `close()` function when you're done with the file.

### `with` and `as`
 - File objects contain special built in methods: `__enter__()` and `__exit__()`.
 - When a file object's `__exit__()` method is invoked, it automatically closes the file.
 - File objects have a `closed` attribute that is `True` when closed and `False` when open.

```python
with open('file.txt', 'r') as textfile:
    textfile.read()
```
