# PythonSnippets
Collection of python code snippets

http://users.uj.edu.pl/~ufkapano/algorytmy/lekcja04/

## Bash getting in the directory where the module is defined
Put it in your .bashrc or .bash_profile and do cdp <python module name> to get in the directory where the module is defined.: 
equals: 
print(os.path.dirname(os.path.realpath(__file__[:-1])))

    cdp () {
        cd "$(python -c "import os.path as _, ${1}; \
                print(_.dirname(_.realpath(${1}.__file__[:-1])))"
            )"
    }

 This work:
 
     ~ $ cdp os
    /usr/lib/python2.7 $

    ~ $ cdp os.path
    /usr/lib/python2.7 $


## Basic bash executing
    #!/usr/bin/python3
   
With Python 3, all strings will be Unicode strings, so the original encoding of the source will have no impact at run-time
    
    # -*- coding: utf-8 -*-
or

    # coding: utf8


## Virtual environment python initialisation
```python
virtualenv -p /usr/bin/python3 py3env
source py3env/bin/activate
pip install package-name
```


## Configuration file for your project app
```python
import os

def read(fname):
    try:
        return open(os.path.join(os.path.dirname(__file__), fname)).read()
    except IOError:
        return ''

configuration = [line for line in read('requirements.txt').split('\n')
                        if line and not line.startswith('#')],
print(configuration)
```


# Statements


## List comprehensions
```python
[i for i in range(10) if i % 2 == 0]
```


## Zip List comprehensions
```python
[item for item in zip([1, 2, 3], [4, 5, 6])]
```


## Results of zip() can be reversed by another zip()
```python
[item for item in zip(*zip([1, 2, 3], [4, 5, 6]))]
```


## Set comprehensions
```python
{item for item in iterable if condition}
```


## Dictionary comprehensions
```python
{key:value for key, value in [[1,2],[3,4],[5,6]]}
```


## Generator expression/comprehension
```python
gen = (item for item in (1, 2, 3))
next(gen)
next(gen)
next(gen)
```


## Open file with generator
```python
csv_gen = (row for row in open('file_name.txt'))
next(csv_gen)
```


## String concatenation
```python
'\n'.join(['some', 'comma', 'separated', 'values'])
```


## Enumerate List comprehension
```python
[(i, j) for i, j in enumerate(["one", "two", "three"])]
```


## Reverse String but skip
```python
gen = (t for t in reversed("abcdef") if t not in "a")
```


## Reverse String but skip given char
```python
string = "abcdef"
parameter = ["a", "f"]  #  Skip reversing
generator = (t for t in reversed(string) if t not in parameter)
''.join(t if t in parameter else next(generator) for t in string)
```


## Lambda FizzBuzz
```python
map(lambda i: "Fizz"*(i%3==0)+"Buzz"*(i%5==0) or str(i), range(1,101))
```


# OS


## Open file / Read file / Manage file input
```python
try:
    with open("file.txt", "r") as file:
        # Everyting
        print (file.read())

        # Line by line
        print (file.readlines()) 

except IOError:
    print("File not found")
```


## Append to file
```python
with open("test.txt", "a") as file:
    file.write("appended text")
```


## Count character occurences in a file
```python
f = open('file.csv','r')
for line in f:
    counter = line.count('x')
    if counter != 5:
        print(line)
    else:
        pass
```


## Manage file input with OS
```python
import os

def read(fname):
    return open(os.path.join(os.path.dirname(__file__), fname)).read()

print(read("C:\Users\username\Desktop\README.txt"))
```


## Recursive directory walk
```python
import os
import sys

print('walk_dir = ' + walk_dir)
print('walk_dir (absolute) = ' + os.path.abspath(walk_dir))

for root, subdirs, files in os.walk(walk_dir):
    print('--\nroot = ' + root)
    print('list_file_path = ' + list_file_path)
    for subdir in subdirs:
        print('\t- subdirectory ' + subdir)

    for file_name in files:
        file_path = os.path.join(root, file_name)

        print('\t- file %s (full path: %s)' % (file_name, file_path))

        with open(file_path, 'rb') as file:
            file_content = file.read()
            print(file_content)
```


## Load multiple files
```python
import glob

PATH = "HOTELS\*.txt"

files = glob.glob(PATH)
for name in files:
    try:
        with open(name) as file:
            file_name = name.split('\\')
            file_name = file_name[1]
            print(file_name)
            #content = file.read()
            #print(content)
        
    except IOError as e:
        print(e)
```


## Write Load CSV file
```python
import csv

filename = r'filename.csv'


DATA = [
    {'sepal_length': 5.4, 'sepal_width': 3.9, 'petal_length': 1.3, 'petal_width': 0.4, 'species': 'setosa'},
    {'sepal_length': 5.9, 'sepal_width': 3.0, 'petal_length': 5.1, 'petal_width': 1.8, 'species': 'virginica'},
    {'sepal_length': 6.0, 'sepal_width': 3.4, 'petal_length': 4.5, 'petal_width': 1.6, 'species': 'versicolor'},
    {'sepal_length': 7.3, 'sepal_width': 2.9, 'petal_length': 6.3, 'petal_width': 1.8, 'species': 'virginica'},
    {'sepal_length': 5.6, 'sepal_width': 2.5, 'petal_length': 3.9, 'petal_width': 1.1, 'species': 'versicolor'},
    {'sepal_length': 5.4, 'sepal_width': 3.9, 'petal_length': 1.3, 'petal_width': 0.4, 'species': 'setosa'},
]

# Write CSV
with open(filename, mode='w') as file:
    writer = csv.DictWriter(
        f=file,
        fieldnames=['sepal_length', 'sepal_width', 'petal_length', 'petal_width', 'species'],
        delimiter=',',
        quotechar='"',
        quoting=csv.QUOTE_ALL,
        lineterminator='\n')

    writer.writeheader()

    for row in DATA:
        writer.writerow(row)

# Open CSV
with open(filename) as file:
    data = csv.DictReader(file, delimiter=',', quotechar='"')

    for line in data:
        print(dict(line))
```


# Script Writing


## Verbose Mode

```python
#Python 2.x

if verbose:
    def verboseprint(*args):
        # Print each argument separately so caller doesn't need to
        # stuff everything to be printed into a single string
        for arg in args:
           print arg,
        print
else:   
    verboseprint = lambda *a: None      # do-nothing function


#Python 3.x

verbose = True
vprint = print if verbose else lambda *a, **k: None
vprint("hello world")
```


# Automate Testing


## Any
```python
data= True
id = None
time = True
group = True

var = any(v is None for v in (data, id, time, group))
print(var)
```


## Assert
```python
def inc(x):
    return x + 1

def test_answer():
    assert inc(3) == 5

print(test_answer())
```


## Try, Except, Finally - error handling
```python
x=0
try:
    print(1/x)

except Exception as e:
    print("Error: " + str(e))

finally:
    x = 1
    print("Lets try anway with:  " + str(x) )
    print("Answer is " + str(1/x) )
```


## Try if, Except
```python
succeed = False
try:
    if succeed is True:
        print("Yay!")

    elif succeed is False:
        raise Exception("No succeed ;(")
finally:
    print("But we execute finally anyway")
```


# Strings


## Split phrase into words
```python
PHRASE = "Would you like to know more?"
num_words = len(PHRASE.split(" "))
print("There are {:} words in {:}".format(num_words, PHRASE))

#or

PHRASE = "Would you like to know more?"
print("There are %s words in %s" % (PHRASE.count(' ') + 1, PHRASE))
```


## In this case it's just the regular multiplication operator. In Python you can multiply strings by ints:
```python
print( "hello" * 3 )
#hellohellohello
```


## Python can also implicitly convert between bools and ints, where True is 1 and False is 0, making this sort of thing work:
```python
print( "hello" * True )
#"hello"
    
print( "hello" * False ) 
```


# Numbers


## Binary Number tricks
```python
num = 21

# 0x hexadecimal (base 16) Notification
'{:0x}'.format(num)  # '15'
print(0x15)

# Octal
'{:0o}'.format(num)  # '25'

# Binary
'{:016b}'.format(num)  # '0000000000010101'

# Binary Reversed
'{:016b}'.format(num)[::-1]  # '1010100000000000'

# Convert to numbers, by providing the expected base (16 for hexadecimal numbers)
int("12ef", 16)

# XOR hex numbers 'ABCD' to '12EF'. answer = B922
hex(int("12ef", 16) ^ int("abcd", 16))
```


# Dictionaries


## Merge two dictionaries (Python 3.5)
```python
#For dictionaries x and y, z becomes a shallowly merged dictionary with values from y replacing those from x.

x = {"a":1, "b":2}
y = {"a":3, "b":4}

z = {**x, **y}
print(z)
```


## Looping over dictionary keys
```python
# key : value
dictionary = {'matthew':'blue', 'rachel':'green', 'raymond':'red'}

for key in dictionary.keys():
    if key.startswith('r'):
        del dictionary[key]

for key in dictionary:
    print(key)
```


## Access records
```python
data = {
    'customer': {
        'salutation': "mr",
        'first_name': "John",
        'last_name': "Doe",
        'email': "john@example.com",
        'plugin_id': "1",
        'plugin_order': "1",
    },
}

print(data['customer']['salutation'])
print(data['customer']['first_name'])
print(data['customer']['last_name'])
print(data['customer']['email'])
```


## Looping over dictionary keys and values
```python
dictionary = {'matthew':'blue', 'rachel':'green', 'raymond':'red'}
for key, value in dictionary.items():
    print(key + " ---> " + value)

# or Access by key
for key in dictionary:
    print(key + " ---> " + dictionary[key])
```


## Dictionary Comprehensions
```python
my_dict = {'a': [1, 2, 3], 'b': [4, 5, 6]}
my_copy = {key: value[:] for key, value in my_dict.items()}
print(my_copy)
```


## Construct a dictionary from pairs / two lists
```python
names = ['0. Cory', '1. Trevor', '2. Ray', '3. Ricky']
colors = ['0. Red', '1. Green', '2. Blue', '3. Yellow']

dictionary = dict(zip(names, colors))
print(dictionary)
```


## Dictionary mapping characters
```python
normal = u' 0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&()*+,-./:;<=>?@[\\]^_`{|}~'
wide = u'　０１２３４５６７８９ａｂｃｄｅｆｇｈｉｊｋｌｍｎｏｐｑｒｓｔｕｖｗｘｙｚＡＢＣＤＥＦＧＨＩＪＫＬＭＮＯＰＱＲＳＴＵＶＷＸＹＺ！゛＃＄％＆（）＊＋、ー。／：；〈＝〉？＠［\\］＾＿‘｛｜｝～'

def vaporize(text):
    # ord - String to Unicode code point. Example: ord('a') -> int 97
    widemap = dict((ord(x[0]), x[1]) for x in zip(normal, wide))
    return text.translate(widemap)

print(vaporize("aesthetics"))
```


## Parse Separated Values into Single Dictionary
```python
def parse_to_dictionary(text):
    """
        Parses inputs like:
        variable : some value
        variable2 : 123.44
        into dict
    """
    return dict(
        map(lambda kv: (kv[0].rstrip(), kv[1].lstrip()),
            filter(
                lambda l: len(l) == 2,
                map(lambda l: l.split(':', 1),
                    text.splitlines()))
            )
    )
```


# JSON


## Simple Open
```python
import json
with open("secret.json") as f:
    data = json.loads(f.read())
```


## Check if JSON contains key - Open, Edit, Close
```python
import json
import os

#dict2 = {"127.0.0.1": "value",
#        "127.0.0.2": "value",
#        "127.0.0.3": "value"}

dict = {}
exists = os.path.isfile('dict.json')
key = "127.0.0.4"

if exists:
    print("File already exists")
    f = open("dict.json","r")
    dict = json.load(f)

if key in dict:
    x = dict[key]
    print(x)

else:
    print("Not found. Adding key...")
    # Open json file and add Key : Value
    with open('dict.json', 'r+') as f:
        dict = json.load(f)
        dict[key] = "value"           # <--- add value.
        f.seek(0)                     # <--- should reset file position to the beginning.
        json.dump(dict, f, indent=4)
        f.truncate()                  # remove remaining part
```


# XML


## Parse XML File
```python
xml = """<root>
            <Sprawa>
                <PrzebiegSprawy>
                    <Czynnosc>
                        <DataCzynnosci>2018-09-03</DataCzynnosci>
                    </Czynnosc>
                </PrzebiegSprawy>
            </Sprawa>

            <Sprawa>
                <PrzebiegSprawy>
                    <Czynnosc>
                        <DataCzynnosci>2018-09-04</DataCzynnosci>
                    </Czynnosc>
                </PrzebiegSprawy>
            </Sprawa>
        </root>"""

import xml.etree.ElementTree as ET
root = ET.fromstring(xml)
for sprawa in root.findall('Sprawa'):
    data_sprawy = sprawa.find('./PrzebiegSprawy/Czynnosc/DataCzynnosci')
    print(data_sprawy.text)
        
```


# Lists


## List Basics
```python
list = []
value = "value"

# Insert Into The Beginning Of A List In Python
list.insert(0, value)

# Insert Into The End Of A List In Python
list.append(value)

# Insert Into An Existing Index Of A Python List
list[index] = value

# Concatenating Two Python Lists
list_a += list_b
```


## List slicing
```python
list = [0, 1, 2, 3, 4 ,5, 6, 7, 8, 9]

print("all after first")
print(list[1:])

print("all but last two")
print(list[:-2])

print("items with ends removed")
print(list[1:-1])

print("items reversed")
print(list[::-1])

print("the first two items, reversed")
print(list[1::-1])

print("the last two items, reversed")
print(list[:-3:-1])

print("everything except the last two items, reversed")
print(list[-3::-1])

print("all even indexes")
print(list[::2])

print("all odd indexes")
print(list[::3])
```


## Detect If Item is the Last in a List
```python
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 14, 56]

my_list_len = len(my_list)-1
for index, x in enumerate(my_list):
    if index == my_list_len:
        print("Last is: " + str(x))
```


## List Difference / Remove from List A values from List B
```python
A = [1, 2, 3, 4, 5]
B = [2, 4, 6]

C = list(set(A) - set(B))
print(C)

#or

foo = [x for x in A if x not in B]
print(foo)
```


## "List Index Out Of Range" Error
```python
def my_function(list):
    try:
        third_value = list[2]
    except IndexError:
        print(f'list has only {len(list)} elements')
        raise

my_function([1,2])
# list has only 2 elements
# IndexError: list index out of range
```


## Looping over over List: two collections
```python
names = ['0. Cory', '1. Trevor', '2. Ray', '3. Ricky']
colors = ['0. Red', '1. Green', '2. Blue', '3. Yellow']

for name, color in zip(names, colors):
    print (name + " ---> " + color ) 
```


## Zip Lists
```python
products = ["Coat", "Jacket", "Shirt"]
prices = [50, 30, 5]
colors = ["white", "black", "magenta"]

for (product, price, color) in zip(products, prices, colors):
    print(f"{product} is {color} and costs ${price:.2f}")
```


## Looping over List in sorted order
```python
colors = ['0. Red', '1. Green', '2. Blue', '3. Yellow']
for color in sorted(colors):
    print(color)

for color in sorted(colors, reverse=True):
    print(color)
```


## Custom sort order
```python
colors = ['0. Red', '1. Green', '2. Blue', '3. Yellow']
def compare_length(c1, c2):
    if len(c1) < len(c2):
        return -1
    if len(c1) > len(c2):
        return 1
    return 0

print(sorted(colors, cmp=compare_length))
```


## Remove char at specific index
```python
string_to_check = "??blahblah123123123"
chars = ["?","a"]

def remove_at(i, s):
    """
        Remove char at specific index
    """
    return s[:i] + s[i+1:]

if string_to_check[0] in chars:
    new = remove_at(0, string_to_check)
    print(string_to_check)
    print(new)

else:
    print("Nothing found")
```


## Appending functions to list
```python
functions = []
for i in range(10):
    functions.append(lambda i=i: i)

#print(*functions)

for f in functions:
    print(str(f()) + " " + str(f))
```


## Tuples inside list
```python
names = [('Anna', 1), ('Jenny', 2)]
for (name, id) in names:
    print(name + " " + str(id))
```


## Using enumerate for loops (range) if you need an index
```python
list = ["a", "b", "c", "d", "e"]
for index, element in enumerate(list):
    print("index: {}, element: {}".format(index, element))
# index: 0, element: a
# index: 1, element: b
# index: 2, element: c
# index: 3, element: d
# index: 4, element: e
```


## Using enumerate for loops, count elements from 1
```python
myList = ["a","b","c","d","e"]
for count, element in enumerate(myList, 1):
    print(f"{count}) {element}")
```


## Using enumerate to replace
```python
string = "abcdefghijk"
guid = 16 * ["-"]
# guid = ['-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-']
for i, x in enumerate(string):
    guid[i] = x # or conversion int(x)

print(guid)
# guid = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', '-', '-', '-', '-', '-']
```


## f-strings (new in Python 3.6)
```python
things = ["a", "b", "c", "d", "e"]
for i, thing in enumerate(things):
    print(f"index: {i}, thing: {thing}".)
```


## List Flattening
```python
nest = [[1, 2], [3, 4], [5, 6]]

# Using chain

from itertools import chain
list(chain.from_iterable(nest))
#[1, 2, 3, 4, 5, 6]

# Using sum

sum(nest, [])
#[1, 2, 3, 4, 5, 6]

# Using List Comprehensions

[l for n in nest for l in n]
# [1, 2, 3, 4, 5, 6]
```


## Check if all elements of a list matches a condition
```python
items = [[1, 1, 1], [1, 2, 2], [1, 3, 3]]
all(item[0] == 1 for item in items)
# True

items = [[1, 1, 1], [1, 1, 1], [1, 1, 1]]
all(item == [1,1,1] for item in items)
# True
```


## Check if at least one element of a list matches a condition
    items=[True, True, True, True]
    any(item == False for item in items)
False

    items=[True, True, True, False]
    any(item == False for item in items)
True


## Find all indexes
    def all_indices(value, list):
        indices = []
        idx = -1
        while True:
            try:
                idx = list.index(value, idx+1)
                indices.append(idx)
            except ValueError:
                break
        return indices

    items = [True, True, False, False]

    all_indices(True, items)
[0, 1]


## Apply A Function To A List with List Comprehensions
    original_list = [1,2,3,4,5]
    double_list = [element * 2 for element in original_list]
[2, 4, 6, 8, 10]


## Apply A Function To A List under condition (equals 0) with List Comprehensions
    def is_zero(arg):
        if arg is 0:
            return True
        else:
            return False

    lines = [0, 0, 1, 0, 0, 1]
    visible = [line + 10 for line in lines if is_zero(line)]
    print(visible)
[10, 10, 10, 10]


## Find all indexes with List Comprehensions
    items = [True, True, False, False]
    indexes = [i for i, e in enumerate(items) if e == True]
[0, 1]


## Remove all negative numbers and every third number with List Comprehensions
```python
list = [1, 2, 3, 4, 5, 6, -1, 8, 9, 10, -2, 5]
# Show me all numbers that are greater or equal 0 and each index is not mod 3 = 2
print([x for i, x in enumerate(list) if x >= 0 and i % 3 != 2]) 

# 0 % 3 = 0
# 1 % 3 = 1
# 2 % 3 = 2 <-- 3 element

# 3 % 3 = 0
# 4 % 3 = 1
# 5 % 3 = 2 <-- 3 element
```
[1, 2, 4, 5, 8, 10]


# Functions


## *ARGS


```python
def AVG(*wages):
    i = 0 # count them
    sum = 0.0 #sum them

    for w in wages:
        i+=1
        sum+=w
    else:
        print('No wages given')
    print(sum/i)

AVG(1,2,3)
```


## Call function by it's name
```python
def printer(text):
    print(text)

locals()["printer"]("Print this")

globals()["printer"]("Global printer")
```


## Call function attribute by it's name
```python
import time

method_to_call = getattr(time, 'clock') #  time.clock()
result = method_to_call()
print(result)
```


## Call function attribute with an argument by it's name
```python
import math

method_to_call = getattr(math, 'fabs') #  math.fabs(x) Return the absolute value of x.
result = method_to_call(-1)
print(result)
```


## Call function attribute with Eval
```python
import math

def get_attribute(attribute):
    # Check if function has an attribute
    if hasattr(math, attribute):
        # Return module.attribute
        return eval("math." + attribute)

# Call it
print(get_attribute("fabs"))
# Use it
print(get_attribute("fabs")(-1))
```


# Lambdas


## Assign Name to lambda
```python
func1 = lambda x, y, z: x + y + z
print(func1(2, 3, 4))

# same as

def func1(x, y, z):
    return x + y + z
```


# Default argument in lambda
```python
func2 = (lambda x=0, y=0, z=0: x + y + z)
print(func2(4, 5))
```


# Use lambda in map()
```python
my_list = map(lambda x: 2*x+1, range(9))
print(", ".join(str(i) for i in my_list))

my_list = [2*x+1 for x in range(9)]
print(my_list)
```

# Build dictionary or list with lambda
```python
# dictionary
action = {
"one": lambda x: x,
"two": lambda x: x**2,
"three": lambda x: x**3
}
print(action["two"](10))  # pow(10, 2) = 100

# list
powers = [
lambda x : 1,
lambda x: x, 
lambda x: pow(x, 2), 
lambda x: pow(x, 3)
]
print(powers[2](3))  # pow(3, 2) = 9

```


# Lambda Choice logic
```python
lambda_abs = lambda x: -x if x < 0 else x
lambda_min = lambda x, y: x if x < y else y
lambda_max = lambda x, y: x if x > y else y

print(lambda_abs(-1))
print(lambda_min(2, 1))
print(lambda_max(2, 1))
```


# Decorators


## Simple decorator
```python
# Decorator is just a function that takes another function as an argument
"""
    @decorator
    def func():
        ...

    expands to

    def func():
        ...
    func = decorator(func)
"""

def get_function_name_dec(func):
  def wrapper(*arg):
      function_returns = func(*arg)  # What our function returns
      return func.__name__ + ": " + function_returns

  return wrapper

@get_function_name_dec
def hello_world():
    return "Hi"

print(hello_world())
```


## Decorator Measure elapsed time 
```python
import time

def time_dec(func):
  def wrapper(*arg):
      start = time.time()
      res = func(*arg)
      print('%r %2.2f ms ' % (func.__name__, (time.time() - start) * 1000 ))
      return res

  return wrapper

@time_dec
def run(n, k):
    return n**k

print(run(2, 10000))
print(run(2, 100000))
```


## Parametrizing decorators
def repeat(number=3):
    """Cause decorated function to be repeated a number of times.
    Last value of original function call is returned as a result
    :param number: number of repetitions, 3 if not specified
    """
    def actual_decorator(function):
        def wrapper(*args, **kwargs):
            result = None
            for _ in range(number):
                result = function(*args, **kwargs)
            return result
        return wrapper
    return actual_decorator

@repeat()
def foo():
    print("foo")

foo()




# Classes


## Simple class
```python
class Dog():
    """Represent a dog."""

    def __init__(self, name):
        """Initialize dog object."""
        self.name = name

    def sit(self):
        """Simulate sitting."""
        print(self.name + " is sitting.")

my_dog = Dog('Peso')

print(my_dog.name + " is a great dog!")
my_dog.sit()
```


## Properties vs. Getters and Setters
```python
from random import randint

class User(object):
    """
    @property: Create functions for managing the getting, setting and deleting of an attribute. 
    """

    def __str__(self):
       """
           Special "Dunder method" called by class, when class is used as a string
       """
       return "This is instance of User class"
 
    def __init__(self, name, password):
        self.__name = name
        self.__password = password
        self.__gold = 10
        self.__level = 1
        self.__power = randint(0, 5)  # random power between 0 and 5

    @property
    def power(self):
        return self.__power

    # Name
    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, new_name):
        self.__name = new_name

    # Gold
    @property
    def gold(self):
        return self.__gold
 
    @gold.setter
    def gold(self, new_gold):
        try:
            self.__gold = int(new_gold)
        except ValueError, TypeError:
            print('Must be an integer')
            raise

if __name__ == "__main__":
    # Create new instance of User Class
    user = User(name='Mike', password='123')
    print(user)
    print(user.name)
    print(user.gold)

    # Set User Attribute Gold
    user.gold = 2222
    print(user.gold)

    # Set User Attribute Name
    user.name = "Steve"
    print(user.name) # User Attribute

    # 
    print(user.power)
```


## Instance, Class, and Static Methods


```python
class Pizza:
    def __init__(self, ingredients):
        self.ingredients = ingredients

    def __repr__(self):
        return f'Pizza({self.ingredients!r})'

    @classmethod
    def margherita(cls):
        return cls(['mozzarella', 'tomatoes'])

    @classmethod
    def prosciutto(cls):
        return cls(['mozzarella', 'tomatoes', 'ham'])
```


## Class method works and inheritance
```python
from datetime import date

# random Person
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @staticmethod
    """
    @staticmethod: A method that does not receive the implicit argument self as a first argument.
    """
    def fromFathersAge(name, fatherAge, fatherPersonAgeDiff):
        return Person(name, date.today().year - fatherAge + fatherPersonAgeDiff)

    @classmethod
    """
    @classmethod: A method that receives the class as an implicit argument instead of the instance.
    """
    def fromBirthYear(cls, name, birthYear):
        return cls(name, date.today().year - birthYear)

    def display(self):
        print(self.name + "'s age is: " + str(self.age))

class Man(Person):
    sex = 'Male'

man = Man.fromBirthYear('John', 1985)
print(isinstance(man, Man))

man1 = Man.fromFathersAge('John', 1965, 20)
print(isinstance(man1, Man))
```


## Class __str__ vs __repr__
```python
class Time:
    def __init__(self, seconds=0):
        self.s = seconds

    def __str__(self):
        """If there is no str method, repr will be used in this place"""
        return "%s sec" % self.s

    def __repr__(self):
        """reproducts the object"""
        return "Time(%s)" % self.s

time1 = Time(12)
time2 = Time(3456)

print(time1, time2)      # Execute str()
print([time1, time2])    # Execute repr() (list)
print({time1, time2})    # Execute repr() (set)
```


# Recursion


## Recursively printing n lines with an asterisk
```python
def print_stars(n):
    if n > 0:
        print("*")
        print_stars(n-1)

print_stars(5)
```


## Recursive calculation of the factorial function n!
```python
# 0! = 1, 1! = 1, n! = n*(n-1)!

def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n-1)

import math
print (math.factorial(10) == factorial(10))
```


## Reverse String
```python
def reverse(s):
    if len(s) == 0:
        return s
    else:
        return reverse(s[1:]) + s[0]
s = "Hello"
print(reverse(s))

# Notice that it's not just s[1:] + s[0], it's reverse(s[1:]) + s[0]. That means:
# reverse('hello') calls reverse('ello') and then adds the 'h'
# reverse('ello') calls reverse('llo') and then adds the 'e'
# reverse('llo') calls reverse('lo') and then adds the 'l'
# reverse('lo') calls reverse('o') and then adds the 'l'
# reverse('o') calls reverse('') and then adds the 'o'
# reverse('') returns '' because len('') == 0.
```


# Time


## Converting an epoch time to a datetime object:
```python
def epoch_to_dt(epoch):
    return datetime(*gmtime(epoch)[:6])
```


## Converting an epoch time to a readable format:
```python
print(str(time.strftime("%H:%M:%S", time.gmtime(1546599577) )))
# 10:59:37

print(str(time.strftime("%I:%M %p", time.gmtime(1546599577) )))
# 10:59 AM

print(str(time.strftime("%d-%m-%Y %H:%M:%S", time.gmtime(1546599577) )))
# 04-01-2019 10:59:37

print(str(time.strftime("%A %d-%m-%Y %H:%M:%S", time.gmtime(1546599577) )))
# Friday 04-01-2019 10:59:37

print( datetime.datetime.fromtimestamp(float(1546599577099)/1000).strftime('%Y-%m-%d %H:%M:%S.%f') )
# 2019-01-04 11:59:37.099000
```


# Matplotlib Library


## Basic Plot
```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 2.5])
plt.ylabel('some numbers')
```


## Customized basic plot
```python
import matplotlib.pyplot as plt
# [x][y]
plt.plot([1, 2, 3, 4], [10, 20, 25, 30], color='lightblue', linewidth=3)
plt.scatter([1,2,3], [4,5,6], color='darkgreen', marker='^')

plt.xlim(0.5, 4.5)
plt.title("Title of the plot")
plt.xlabel("This is the x-label")
plt.ylabel("This is the y-label")
```


## Generate data and plot
```python
import matplotlib.pyplot as plt
# np.linspace - Return evenly spaced numbers over a specified interval.
x = np.linspace(-np.pi, np.pi, 200)
sine = np.sin(x)
cosine = np.cos(x)

fig, ax = plt.subplots()
ax.plot(x, sine, x, cosine)
```


# SYS Library


## Terminal SYS argv
```python
import sys

# using variable name _ by convention to note that we don't care about sys.argv[0] (name of our program)
_, first_argument, second_argument = sys.argv
print(f"filename:  {_}")
print(f"first argument: {first_argument} second argument: {second_argument}")

#>python argv.py a b
```


## Terminal SYS Simple Loading
```python
import time
import sys

for x in range (0, 5):  
    b = "Loading" + "." * x
    sys.stdout.write("\r" + b)
    time.sleep(1)
```


## Terminal SYS Simple Repeat Loading
```python
import time
import sys

for x in range (0, 5):  
    b = "Loading" + "." * x
    for i in ["Loading", "Loading.", "Loading..", "Loading..."]:
        sys.stdout.write("\r" + i)
        sys.stdout.write("\033[K")
        time.sleep(1)
```


## Terminal SYS Counter
```python
import time
import sys

counter = 0
Done = False

while not Done:
    #print(counter)
    sys.stdout.write("\r " + str(counter))
    sys.stdout.flush()
    counter +=1
    if counter == 10:
        Done = True
    time.sleep(1) # each one sec
```


## Terminal SYS Flush two lines at the same time
```python
import sys
from random import randint
import time

CURSOR_UP_ONE = '\x1b[1A'
ERASE_LINE = '\x1b[2K'

while True:
    data_on_first_line = CURSOR_UP_ONE + ERASE_LINE + str(randint(100, 999)) + "\n"
    data_on_second_line = str(randint(100, 999)) + "\r"
    
    sys.stdout.write(data_on_first_line)
    sys.stdout.write(data_on_second_line)
    sys.stdout.flush()
    time.sleep(1)
```


## Terminal SYS Measuring elapsed time / timer
```python
import time
import sys

counter = 0
Done = False

start_time = time.time()
while not Done:
    #print(counter)
    elapsed_time = time.time() - start_time

    sys.stdout.write("\r " + "Elapsed time: " + str(time.strftime("%H:%M:%S", time.gmtime(elapsed_time))))
    sys.stdout.flush()
    time.sleep(1)
```


## Terminal SYS Progress Bar
```python
import time
import sys

toolbar_width = 40

# setup toolbar
sys.stdout.write("[%s]" % (" " * toolbar_width))
sys.stdout.flush()
sys.stdout.write("\b" * (toolbar_width+1)) # return to start of line, after '['

for i in xrange(toolbar_width):
    time.sleep(0.1) # do real work here
    # update the bar
    sys.stdout.write("-") # try: (u"█")
    sys.stdout.flush()
```


## Terminal SYS Progress Bar With Percentage
```python
from time import sleep
import sys

for i in range(21):
    sys.stdout.write('\r')
    sys.stdout.write("[%-20s] %d%%" % ('-'*i, 5*i))
    sys.stdout.flush()
    sleep(0.25)
```


## Terminal SYS Spinning (rotating) Cursor
```python
import time
import sys

def spinning_cursor():
    while True:
        for cursor in '|/-\\':
            yield cursor

spinner = spinning_cursor()
for _ in range(50):
    sys.stdout.write(next(spinner))
    sys.stdout.flush()
    time.sleep(0.1)
    sys.stdout.write('\r')
```


# Threading


## Creating Threads
```python
import threading
import random
import time
import sys

# sys output line codes
CURSOR_UP_ONE = '\x1b[1A'
ERASE_LINE = '\x1b[2K'


class MyThread(threading.Thread):
    def __str__(self):
        ''' Return str representation'''
        return self.getName()
    
    def __init__(self, val):
        ''' Constructor '''
 
        threading.Thread.__init__(self)
        self.val = val
        self.signal = threading.Event()
        self.period = 5

    def run(self):
        ''' Main run loop '''
        while True:
            if self.signal.is_set():  # Stop if signal is set
                break

            if self.val == 15: # Inside Stop if val == 15
                break
            
            self.val += 1
         
            # Sleep for random time between 1 ~ 5 second
            secondsToSleep = random.randint(1, 5)
            time.sleep(secondsToSleep)

    def stop(self):
        ''' Stop thread by sending signal '''
        self.signal.set()
        self.join(timeout=self.period)
        if self.is_alive():
            raise threading.ThreadError("Stopping thread failed")


if __name__ == '__main__':
    # Declare objects of MyThread class
    myThreadOb1 = MyThread(4)
    myThreadOb2 = MyThread(4)
    
    # Set thread name
    myThreadOb1.setName('Thread 1')
    myThreadOb2.setName('Thread 2')

    # Start running the threads!
    myThreadOb1.start()
    myThreadOb2.start()
    
    while True:
        #sys.stdout.write('T: %s value: %d' % (myThreadOb1.getName(), myThreadOb1.val))
        #sys.stdout.write('\r' + 'T: %s value: %d' % (myThreadOb2.getName(), myThreadOb2.val))
        
        first_line = CURSOR_UP_ONE + ERASE_LINE + myThreadOb1.getName() + " Value: " + str(myThreadOb1.val) + " Alive: " + str(myThreadOb1.is_alive()) + "\n"
        second_line = myThreadOb2.getName() + " Value: " + str(myThreadOb2.val) + " Alive: " + str(myThreadOb2.is_alive()) + "\r"

        sys.stdout.write(first_line)
        sys.stdout.write(second_line)
        sys.stdout.flush()
        time.sleep(1)

        # Send signal to stop threads if:
        if myThreadOb1.val == 6:
            myThreadOb1.stop()

        if myThreadOb2.val == 6:
            myThreadOb2.stop()

        # Quit refreshing Loop if all threads are dead
        if all(item == False for item in [myThreadOb1.is_alive(), myThreadOb2.is_alive()]):
            break

    sys.stdout.write("\n" + "Terminating..." + "\r")
```


## Manage multiple threads
```python
import threading
import time

def sleeper_thread(seconds, name):
    print('{}: Hi, I am {}. Going to sleep for {} seconds \n'.format(name, name, seconds))
    time.sleep(seconds)

    print('{}: I just woke up \n'.format(name))
    print('{}: hello'.format(name))
    print('{}: what is going on'.format(name))
    print('---------------------------------- \n')

t1 = threading.Thread(target = sleeper_thread, name = 'thread1', args = (10, 'thread1') )
t2 = threading.Thread(target = sleeper_thread, name = 'thread2', args = (15, 'thread2') )

t1.start() # Start the thread’s activity
print('{} is alive \n'.format(t1))
t2.start() # Start the thread’s activity
print('{} is alive \n'.format(t2))

t1.join() # Wait until the thread terminates
print('{} died'.format(t1))
t2.join() # Wait until the thread terminates
print('{} died'.format(t2))
```


## Multithreading from Dictionary / looping over Threads

```python
# Create multiple different functions,
# then use the value of Targets to disable their runs.

import threading

def foo():
    print("foo was here")

def bar():
    print("bar was here")

def baz():
    print("baz was here")

# Enable: 1/ Disable: 0
Targets = {foo: 0, bar: 1, baz: 1}

for Loop, Enabled in Targets.items():
    if Enabled == 1:
        print(" Starting up " + str(Loop))
        print("   Enabled? " + str(bool(Enabled)))
        thread = threading.Thread(target=Loop)
        thread.daemon = True
        thread.start()
        thread.join()
else:
    print(" Skipping " + str(Loop))
```


# Coroutines
```python
import asyncio

async def compute1():
    for i in range(5):
        print('compute1 %d' % i)
        await asyncio.sleep(.1)

async def compute2():
    for i in range(5):
        print('compute2 %d' % i)
        await asyncio.sleep(.2)

async def main():
    await asyncio.gather(compute1(), compute2())
    print("Done")

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
loop.close()
```


# Socket


## Simple UDP Client - Server
```python
# UDP Client

import socket

HOST = '127.0.0.1'
PORT = 1337

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)  # SOCK_DGRAM specifies datagram (udp) sockets.
s.connect((HOST, PORT))

s.send('Hello World 1')
s.send('Hello World 2')
s.send('Hello World 3')
```


```python
# UDP Server

import socket

HOST = '127.0.0.1' # 0.0.0.0 - listen on all network cards
PORT = 1337

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)  # SOCK_DGRAM specifies datagram (udp) sockets.
s.bind((HOST, PORT))

print("Waiting on port: " +  str(PORT))
while True:
    data, addr = s.recvfrom(1024)
    print(data)
    print(addr) # client PORT and HOST
```


## Simple TCP Client - Server
```python
# TCP Client

import socket

HOST = '127.0.0.1'
PORT = 12345

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  
sock.connect(HOST, PORT)  

sock.send(b"Hello World from Client")  

print(sock.recv(1024))
sock.close()
```

```python
# TCP Server

import socket

HOST = '127.0.0.1'
PORT = 12345

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  
sock.bind(HOST, PORT)
sock.listen(5)

print("Server is running...")
while True:
    connection, address = sock.accept()  
    buf = connection.recv(1024)  
    print(buf)
    connection.send(buf)    		
    connection.close()
```


## Send File Via UDP
```python
# Sender

import socket
import sys

HOST = '127.0.0.1'
PORT = 9999
BUFF = 1024
file_name = 'test.txt'

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
addr = (HOST, PORT)

s.sendto(file_name, addr)

f = open(file_name,"rb")
data = f.read(BUFF)
while (data):
    if(s.sendto(data, addr)):
        print("Sending ...")
        data = f.read(BUFF)
s.close()
f.close()
```

# Receiver
```python
import socket
import select

HOST = "127.0.0.1" #  UDP_IP
PORT = 5005 #  IN_PORT 
timeout = 3

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
sock.bind((HOST, PORT))

while True:
    data, addr = sock.recvfrom(1024)
    if data:
        print "File name:", data
        file_name = data.strip()

    f = open(file_name, 'wb')

    while True:
        ready = select.select([sock], [], [], timeout)
        if ready[0]:
            data, addr = sock.recvfrom(1024)
            f.write(data)
        else:
            print "%s Finish!" % file_name
            f.close()
            break
```


## Send File Via TCP
```python
# Sender

import socket

TCP_IP = "127.0.0.1"
FILE_PORT = 5005
DATA_PORT = 5006
buf = 1024
file_name = "picture.png"


try:
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.connect((TCP_IP, FILE_PORT))
    sock.send(file_name)
    sock.close()

    print(f"Sending {file_name}...")

    f = open(file_name, "rb")
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.connect((TCP_IP, DATA_PORT))
    data = f.read()
    sock.send(data)

finally:
    sock.close()
f.close()
```


```python
# Receiver

import socket

TCP_IP = "127.0.0.1"
FILE_PORT = 5005
DATA_PORT = 5006
timeout = 3
buf = 1024


sock_f = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock_f.bind((TCP_IP, FILE_PORT))
sock_f.listen(1)

sock_d = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock_d.bind((TCP_IP, DATA_PORT))
sock_d.listen(1)


while True:
    conn, addr = sock_f.accept()
    data = conn.recv(buf)
    if data:
        print(f"File name: {data}")
        file_name = data.strip()

    f = open(file_name, 'wb')

    conn, addr = sock_d.accept()
    while True:
        data = conn.recv(buf)
        if not data:
            break
        f.write(data)

    print(f"Finish! {file_name}")
    f.close()
```


## Simple TCP Multithread Echo Client - Server
Client

```python
import socket

HOST = "127.0.0.1"
PORT = 1337

# Create an ipv4 (AF_INET) socket object using the tcp protocol (SOCK_STREAM)
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

s.connect((HOST, PORT))

s.send('Hello World Echo')

# 4096 is recommended buffer size
response = s.recv(4096)

print(response)
```

Server

    from socket import *
    import thread

    HOST = '127.0.0.1'
    PORT = 9999
    BUFF = 1024
    
    def response(key):
        return 'Server response: ' + key

    def handler(s_client,addr):
        while True:
            data = s_client.recv(BUFF)
            if not data: break

            print repr(addr) + ' recv:' + repr(data)
            s_client.send(response(data))

            print repr(addr) + ' sent:' + repr(response(data))

            if "close" == data.rstrip(): break # type 'close' on client console to close connection from the server side

        s_client.close()
        print(str(addr) + "- closed connection")

    if __name__=='__main__':
        ADDR = (HOST, PORT)
        s_server = socket(AF_INET, SOCK_STREAM)
        s_server.setsockopt(SOL_SOCKET, SO_REUSEADDR, 1)
        s_server.bind(ADDR)
        s_server.listen(5)
        while True:
            print('Waiting for connection... listening on port: ' + str(PORT))
            s_client, addr = s_server.accept()
            print('...connected from: ' + str(addr))
            thread.start_new_thread(handler, (s_client, addr))

# Selenium

    #!/usr/bin/python3

    from selenium import webdriver
    import os

    #driver loc on disk
    abs_driver = os.path.abspath('/driver/chromedriver')
    ChromeDriverPath = abs_driver

    option = webdriver.ChromeOptions()
    ##option.add_argument("-incognito")
    ##option.add_argument("--start-maximized")
    driver = webdriver.Chrome(executable_path=ChromeDriverPath, chrome_options=option)

    driver.set_window_size(1500, 950)

    driver.get("https://www.site.com/user/login")

    html_addres = driver.current_url
    print(html_addres)

