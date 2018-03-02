# PythonSnippets
Collection of python code snippets

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
    print(configuration[0][2])
