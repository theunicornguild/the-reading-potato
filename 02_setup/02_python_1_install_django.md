  Now, it's time to install `Django`
```shell
(env) $ pip install django
```
`Django` is installed, so now we can create our django project in our current directory.
```shell
(env) $ django-admin startproject reading_potato
```
Let’s look at what `startproject` created:
```
reading_potato/
    manage.py
    db.sqlite3
    reading_potato/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```
Let's explain what these files are:
* `manage.py` contains a bunch of commands/options to interact with the Django project in various ways.
* `db.sqlite3` is the database file that holds the information you will add to your project.
* The inner `reading_potato/` directory is the actual Python package for our project. Basically it's what makes everything work right and together.
* `__init__.py` is an empty file that tells Python that this directory should be considered a Python package.
* `settings.py` is the settings/configuration for the Django project.
* `urls.py` is the URL declarations for this Django project; a “table of contents” of your Django-powered site.
* `wsgi.py` is a file that allows your project to be deployed.


Before we go to the next step, let's try and run the project.
first we'll get into our project's directory. Then we'll use the `runserver` command from `manage.py` to run our server.
```shell
(env) $ cd reading_potato
(env) $ python manage.py runserver
```
You'll see something like this:
Performing system checks...
```shell
System check identified no issues (0 silenced).

You have 14 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.

December 17, 2017 - 09:30:41
Django version 2.0, using settings 'reading_potato.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
Take the URL of the localhost `http://127.0.0.1:8000/` and checkout your website.
Notice that there is a message saying something about unapplied migrations.Django comes with some preconfigured packages that deal with our database. Since we've just gotten these packages we have to apply changes to our database to accommodate for them. This is done by running the migrate command.

However, before you can run any command in the terminal, you have to stop the server first. You can do by pressing the `C` key while holding down the `Ctrl` key.

```shell
(env)$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying sessions.0001_initial... OK
  ```
`manage.py migrate` applies any changes that have been made to the database. So now if we run the server again, we won't see that issue.
```shell
(env)$ python manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).
December 17, 2017 - 09:38:00
Django version 2.0, using settings 'reading_potato.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

### Git

Now that we created the project, we'll initialize it as a git repo and push it to the remote repo you created in the introduction.

```shell
$ git init
$ git add .
$ git commit -m "new project"
$ git push
```
___
