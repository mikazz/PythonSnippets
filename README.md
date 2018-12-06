# PythonSnippets
Collection of python code snippets

## Bash getting in the directory where the module is defined
Put it in your .bashrc or .bash_profile and do cdp <python module name> to get in the directory where the module is defined.:

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


### manage file input

    try:
        with open("file.txt", "r") as file:
            # Everyting
            print (file.read())

            # Line by line
            print (file.readlines()) 

    except IOError:
        print("File not found")

### basic bash executing
    #!/usr/bin/python3
   
With Python 3, all strings will be Unicode strings, so the original encoding of the source will have no impact at run-time
    
    # -*- coding: utf-8 -*-
or

    # coding: utf8

### virtual environment python initialisation
    pip install virtualenv
    virtualenv -p /usr/bin/python3 py3env
    source py3env/bin/activate
    pip install package-name
    
### configuration file for your project app

    import os

    def read(fname):
        try:
            return open(os.path.join(os.path.dirname(__file__), fname)).read()
        except IOError:
            return ''

    configuration = [line for line in read('requirements.txt').split('\n')
                            if line and not line.startswith('#')],
    print(configuration)
    
### default setup script for modules / Setup.py

    from setuptools import setup
    import os
    def read(fname):
        return open(os.path.join(os.path.dirname(__file__), fname)).read()
    setup(
        name = "Project Name",
        version = "0.0.1",
        author = "Author",
        author_email = "author@mail.com",
        description = ("python module"),
        license = "GPLv2",
        keywords = "keyword1 keyword2",
        url = "https://github.com/dantaki/vapeplot/",
        packages=['vapeplot'],
        package_dir={'vapeplot':'vapeplot'},
        long_description=read('README.md'),
        include_package_data=True,
        install_requires=['matplotlib'],
        classifiers=[
            'Development Status :: 3 - Alpha',
            'License :: OSI Approved :: GNU General Public License v2 (GPLv2)',
            'Topic :: Multimedia :: Graphics',
        ],
    )


## Assert
    def inc(x):
        return x + 1

    def test_answer():
        assert inc(3) == 5
    
    print(test_answer())


## Remove char at specific index
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


## Appending functions to list
    functions = []
    for i in range(10):
        functions.append(lambda i=i: i)

    #print(*functions)

    for f in functions:
        print(str(f()) + " " + str(f))


## Tuples inside list
    names = [('Anna', 1), ('Jenny', 2)]
    for (name, id) in names:
        print(name + " " + str(id))


## Using enumerate for loops (range) if you need an index
    things = ["a", "b", "c", "d", "e"]
    for i, thing in enumerate(things):
        print("index: {}, thing: {}".format(i, thing))

    # index: 0, thing: a
    # index: 1, thing: b
    # index: 2, thing: c
    # index: 3, thing: d
    # index: 4, thing: e


## Dictionary mapping characters
    normal = u' 0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&()*+,-./:;<=>?@[\\]^_`{|}~'
    wide = u'　０１２３４５６７８９ａｂｃｄｅｆｇｈｉｊｋｌｍｎｏｐｑｒｓｔｕｖｗｘｙｚＡＢＣＤＥＦＧＨＩＪＫＬＭＮＯＰＱＲＳＴＵＶＷＸＹＺ！゛＃＄％＆（）＊＋、ー。／：；〈＝〉？＠［\\］＾＿‘｛｜｝～'

    def vaporize(text):
        # ord - String to Unicode code point. Example: ord('a') -> int 97
        widemap = dict((ord(x[0]), x[1]) for x in zip(normal, wide))
        return text.translate(widemap)

    print(vaporize("aesthetics"))


## Using enumerate to replace
    given_string = "abcdefghijk"
    guid = 16 * ["-"]
    # guid = ['-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-']
    for i, x in enumerate(given_string):
        guid[i] = x # or conversion int(x)

    print(guid)
    # guid = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', '-', '-', '-', '-', '-']


## Using f-strings (new in Python 3.6)
    things = ["a", "b", "c", "d", "e"]
    for i, thing in enumerate(things):
        print(f"index: {i}, thing: {thing}".)
        

## In this case it's just the regular multiplication operator. In Python you can multiply strings by ints:
    print( "hello" * 3 )


## Python can also implicitly convert between bools and ints, where True is 1 and False is 0, making this sort of thing work:
    print( "hello" * True ) # Prints "hello"
    print( "hello" * False ) # Prints ""


## List Flattening
    nest = [[1, 2], [3, 4], [5, 6]]
    
Using chain

    >>> from itertools import chain
    >>> list(chain.from_iterable(nest))
    [1, 2, 3, 4, 5, 6]

Using sum

    >>> sum(nest, [])
    [1, 2, 3, 4, 5, 6]

Using List Comprehensions

    >>> [l for n in nest for l in n]
    [1, 2, 3, 4, 5, 6]


## Check if all elements of a list matches a condition
    items = [[1, 1, 1], [1, 2, 2], [1, 3, 3]]
    all(item[0] == 1 for item in items)
True

    items = [[1, 1, 1], [1, 1, 1], [1, 1, 1]]
    all(item == [1,1,1] for item in items)
True


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


## Find all indexes with List Comprehensions
    items = [True, True, False, False]
    indexes = [i for i, e in enumerate(items) if e == True]
[0, 1]


## Converting an epoch time to a datetime object:
    def epoch_to_dt(epoch):
        return datetime(*gmtime(epoch)[:6])


## Simple class
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


# Recursion

## Reverse String
    def reverse(s):
        if len(s) == 0:
            return s
        else:
            return reverse(s[1:]) + s[0]
    s = "Hello"
    print(reverse(s))

Notice that it's not just s[1:] + s[0], it's reverse(s[1:]) + s[0]. That means:
reverse('hello') calls reverse('ello') and then adds the 'h',
reverse('ello') calls reverse('llo') and then adds the 'e',
reverse('llo') calls reverse('lo') and then adds the 'l',
reverse('lo') calls reverse('o') and then adds the 'l',
reverse('o') calls reverse('') and then adds the 'o',
reverse('') returns '' because len('') == 0.




# SYS Library


## SYS Counter
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


## SYS Progress Bar
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
        sys.stdout.write("-")
        sys.stdout.flush()


## SYS Spinning (rotating) Cursor
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
