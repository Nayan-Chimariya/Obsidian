## Steps:

1. Create the root folder that will contain your package, it can have the same name as your package:

```bash
mkdir my_package
```

2. Go into the directory and create another directory which will be the package that your are creating and eventually publishing

```bash
cd my_package
mkdir my_package
```

3. Now we need a setup.py file that will have the data required to create our package. This file should be within the root directory **and not in the actual package**

```bash
touch setup.py
```

4. Below is an example on what goes in the setup.py file

```python
from setuptools import setup, find_packages

VERSION = '0.0.0' #specify your version 
DESCRIPTION = 'Time your function' 
LONG_DESCRIPTION = 'A package that allows you to see the runtime of function.'

setup(
    name="functionTime", #the name of your package that you will pip install (required)
    version=VERSION, 
    author="Nayan-Chimariya", #(optional)
    author_email="<cnayan789@gmail.com>", #(optional)
    description=DESCRIPTION, #(optional)
    long_description_content_type="text/markdown", #(optional)
    long_description=LONG_DESCRIPTION, #(optional)
    packages=find_packages(), #(required)
    install_requires=['colorama'], # packages that you import goes here (required)
    classifiers=[ #(optional)
        "Programming Language :: Python :: 3",
        "Operating System :: Unix",
        "Operating System :: MacOS :: MacOS X",
        "Operating System :: Microsoft :: Windows",
    ]
)
```

5. Now that you have created the setup.py file, we can go into the package directory `my_package` and create a special file called `__init__.py` this file tells that the current directory is to be made a package.                                                                                                                                                                                                                                                                                          Create another file named anything other than the your package name, in this case **don't name it my_package** it can cause circular dependency. 
`
```bash
cd my_package
touch __init__.py
touch app.py
```

6. write the functions in `app.py` that you can import later when you pip install your package

```python
def hello():
	print("This is my package")
```

7. In the `__init__.py` file, import the function that you created

```python
from .app import hello
```

**Remember :** The path to your `app.py` has to be absolute, so add a dot ( . ) in front of your file name during import as shown above `.app`

8.  The final structure of your package should look like this 

->package
	->setup.py
	->package
        ->app.py
        ->__init__.py

9. That's it you have created a package, before publishing, test it locally on your system by executing the following 

```python
pip install .
```

10. Test your installation by trying to import your package in the terminal. Type `python` in the terminal and hit enter, this will open the python interactive shell. then try running the following commands

```python
from my_package import hello
```

11. Executing the above command should result in no errors. Once the package has been tested locally, we can now publish it to [Pypi](https://pypi.org/)

12. Create an account in Pypi, verify your email and setup 2 factor authentication without which you cannot publish your packages. Save your API token 

13. Now that you have created the account to Pypi, you are ready to publish your package open your package root directory and open bash from that location. You will need to install two packages; `wheel` `twine` which will be necessary for the push. 

```python
pip install wheel
pip install twine
```

14. After installing those packages, we need to create source distribution `(sdist)` directory and binary distribution `(bdist)` directory, which we will use wheel for. Run the following command on the terminal

```python
python setup.py sdist bdist_wheel
```

15. Now we just need to push the `dist` directory to PyPI. Run the following command 

```python
python -m twine upload dist/*
```

We are running the module `twine` hence we need the -m and we are pushing everything from `dist `so we use *

16. Enter your PyPI  credentials:
	1. Your username has to be` __token__`
	2. Your password is your API key

17. After you successfully publish your package you can run `pip install my_package` which will install your package from Pypi. Since you have already installed your package during testing, requirements already satisfy pops up. Simply uninstall by running 

```python
pip uninstall my_package
```

Then, 

```python
pip install my_package
```
