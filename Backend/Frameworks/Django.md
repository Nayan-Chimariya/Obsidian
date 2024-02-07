### Getting Started
1. Setup environment using any package manager such as [[Conda]]
```python
conda create -n backend python=3.10
```
2. Install Django on that env using the following `pip command`
```python
pip install django
```
3. Create a work directory 'project' and go to that location
```shell
mkdir project
cd project
```
4. Activate the Conda environment
```python
conda activate backend
```
5. Start the project using Django Admin
```python
django-admin startproject project_name .
```
The . specifies that the current folder is to be using as project folder, removing the . will create a redundant folder
6. This will create `manage.py` along with many other files, the `manage.py` is a special file that can perform all actions done by the Django-admin and should be used for further tasks.
7. In order to start the project we run the following command:
```python
python manage.py runserver
```
we can specify port number if the default port 8000 is not available or is being used by other application.

### Creating a new application

A Django application describes a Python package that provides some set of features. Applications may be reused in various projects. Applications include some combination of models, views, templates, template tags, static files, URLs, middleware, etc. They’re generally wired into projects with the INSTALLED_APPS` setting and optionally with other mechanisms such as URLconfs, the MIDDLEWARE` setting, or template inheritance.

Code to create app
```python
python manage.py startapp myapp
```
This will create an application named `myapp` that will contain files such as:
1. Views: used for request handling
2. Urls: Used for mapping urls 
3. models: Used to define schema of the databases

Error I faced during ...
Generic Relationship
