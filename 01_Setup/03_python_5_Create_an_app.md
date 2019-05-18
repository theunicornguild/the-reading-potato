Now, we do have our project, but where do we start writing the code to create our webpages. This is where the `app` comes in.
When talking about a Django app, the term describes a Python package/module that provides some set of features.

Think of Django apps as the building blocks to your Django project.

A project can have several or just one app depending on how you want to organize your project. In this project we'll create two apps:
* `main` : contains all the normal users functionalities.
* `authentication`: contains all authentication related functionalities like login.

we could've done everything in one app but it's nicer and cleaner to divide your code.
Before creating an app make sure your virtual environment is activated and that you are in your project root folder; that's where you can see `manage.py`.
We're using the `startapp` command to create an app and after it we specify the apps name:
```shell
(env) $ python manage.py startapp main
(env) $ python manage.py startapp authentication
```
Let's see the app folders we just created:
```shell
(env)$ ls
reading_potato   db.sqlite3   manage.py  main   authentication
```
This is how the app directory will look like inside of our projects folder
```
main/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
authentication/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
We'll explain each of these components briefly:

* `admin.py` is how we associate the app with the admin page.
* `apps.py` is the app's configuration.
* `migrations` is a folder which holds changes that are made to our database for this app.
* `models.py` is how we map our data to the database.
* `tests.py` is where we can run and design tests for our app.
* `views.py` controls the flow of data in our app.

Every time we create a new app, we need to include it in the `INSTALLED_APPS` list in our `settings.py` file. Open your `settings.py` and find the `INSTALLED_APPS` list.
```python
INSTALLED_APPS = [
		'django.contrib.admin',
		‘django.contrib.auth’,
		‘django.contrib.contenttypes',
		‘django.contrib.sessions',
		‘django.contrib.messages',
		‘django.contrib.staticfiles',
		
		‘main',
		'authentication',
	]
```
the `INSTALLED_APPS` list holds the names of all Django applications that are activated in this Django instance. That is why we need to add our new apps so that your django project can recognize them.
