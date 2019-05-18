To start creating our reading potato project we need to do a few steps:
* Create a virtual environment.
* Install Django.
* Create a new Django project.
* Create a new app.
* Setup the database.

##### Create a virtual environment:

   A virtual environment is basically a folder and when you activate it, it separates everything installed in your computer from your current project. If it still doesn't make sense, think of it like a room, every virtual environment you create in your computer is a seperate room. everything in your room stays in your room unlike an open area where things can get slightly chaotic.
   
   Before we can actually create our virtual environment, we need to install it using `pip` which is a package manager for Python packages. if you dont already have `pip`, you can install it using the following command.
   
   **mac**:
```shell
$ sudo apt-get install python3-pip
```

   **windonws**:
```shell
$ python get-pip.py
```


If you already have `pip`, you can use it to install `virtualenv` which is the tool used to create virtual environments.
```shell
$ pip install virtualenv
```
Now we can finally start creating our virtual environment by using the `virtualenv` command line utility.

**mac**:
```shell
$ virtualenv --python=python3 env
```
**windows**:
```shell
$ virtualenv env
```
`virtualenv --python=python3 env`(in mac) or `virtualenv env`(in windows) will create a folder in the current directory which will contain the Python executable files(in this case, python3), and a copy of the pip library which you can use to install other packages. The name of the virtual environment (in this case, it was env) can be anything. However, this virtual environment will remain just a folder until we activate it. if the virtual environment is a room, you can think of activating it as closing the door. So, first we go into the virtual environment and then we activate it.
```shell
$ cd env
$ source bin/activate
```
notice after activating the virtual environement, the environment's name is shown in brackets on the left hand side.