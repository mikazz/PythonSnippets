# PythonSnippets
Collection of python code snippets

### manage file input

    try:
        with open("file.txt", "r") as file:
            # Everyting
            print (file.read())

            # Line by line
            print (file.readlines()) 

    except IOError:
        print("File not found")

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
    
### default setup script for modules

    """
    Enter name
    ~~~~~~~~
    Enter description
    """

    try:
        from setuptools import setup, find_packages
        have_setuptools = True
    except ImportError:
        from distutils.core import setup
        def find_packages(*args, **kwargs):
            return [
                'Enter package',
                'Enter package',
                'Enter package',
                'Enter package',
                'Enter package',
            ]
        have_setuptools = False

    if have_setuptools:
        add_keywords = dict(
            entry_points = {
                'console_scripts': ['pygmentize = pygments.cmdline:main'],
            },
        )
    else:
        add_keywords = dict(
            scripts = ['pygmentize'],
        )

    setup(
        name = 'Enter name',
        version = 'Enter version',
        url = 'Enter url',
        license = 'Enter License',
        author = 'Enter author',
        author_email = 'Enter mail',
        description = 'Enter description',
        long_description = __doc__,
        keywords = 'Enter kewords',
        packages = find_packages(),
        platforms = 'any',
        zip_safe = False,
        include_package_data = True,
        classifiers = [
            'License :: OSI Approved :: Enter License',
            'Intended Audience :: Developers',
            'Intended Audience :: End Users/Desktop',
            'Intended Audience :: System Administrators',
            'Development Status :: 6 - Mature',
            'Programming Language :: Python',
            'Programming Language :: Python :: 2',
            'Programming Language :: Python :: 3',
            'Operating System :: OS Independent',
            'Topic :: Utilities',
        ],
        **add_keywords
    )
