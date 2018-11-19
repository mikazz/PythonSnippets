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

## Using enumerate for loops (range) if you need an index
    things = ["a", "b", "c", "d", "e"]
    for i, thing in enumerate(things):
        print("index: {}, thing: {}".format(i, thing))

    # index: 0, thing: a
    # index: 1, thing: b
    # index: 2, thing: c
    # index: 3, thing: d
    # index: 4, thing: e

## Using f-strings (new in Python 3.6)
    things = ["a", "b", "c", "d", "e"]
    for i, thing in enumerate(things):
        print(f"index: {i}, thing: {thing}".)

## In this case it's just the regular multiplication operator. In Python you can multiply strings by ints:
    print( "hello" * 3 )
    
## Python can also implicitly convert between bools and ints, where True is 1 and False is 0, making this sort of thing work:
    print( "hello" * True ) # Prints "hello"
    print( "hello" * False ) # Prints ""
