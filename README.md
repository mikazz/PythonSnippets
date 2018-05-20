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

### command line arguments
    import sys
    import getopt

    def main(argv):
       inputfile = ''
       outputfile = ''
       try:
          opts, args = getopt.getopt(argv,"hi:o:",["ifile=","ofile="])
       except getopt.GetoptError:
          print ('test.py -i <inputfile> -o <outputfile>')
          sys.exit(2)

       for opt, arg in opts:
          if opt == '-h':
             print ('test.py -i <inputfile> -o <outputfile>')
             sys.exit()
          elif opt in ("-i", "--ifile"):
             inputfile = arg
          elif opt in ("-o", "--ofile"):
             outputfile = arg

       print ('Input file is "', inputfile)
       print ('Output file is "', outputfile)

    if __name__ == "__main__":
       main(sys.argv[1:])

    
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

