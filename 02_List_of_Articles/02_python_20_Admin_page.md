Now, everything we wrote in our models is applied to the local database. But, how can we see what's inside the database?

`Django` provide what's called an `admin page`, which is a page or a part of your website where you can control all the data saved in your database. you can add/delete/edit any objects that you have saved in your databse. For example, you can access users information, names, emails, usernames, or even add or delete a user. the same can happen for your `Article` model or any other model you decide to create.

To access this page, run the server and then go to this url `http://127.0.0.1:8000/admin/`. you will see a login page. This login page and everything you'll see after you login is precreated by `django`. Since this is the admin page, only `admin` users can access it. So, how do we create an `admin` user, there isn't a register button anywhere, right?

So, we know it's not going to be a normal registeration. instead, we'll go to the terminal and run this command:
```shell
(env)$ python manage.py createsuperuser
Username (leave blank to use <USERNAME>'): <ENTER_YOUR_USERNAME>
Email address: <ENTER_YOUR_EMAIL_OR_LEAVE_BLANK>
Password: <ENTER_YOUR_PASSWORD>
```
what `createsuperuser` does is create a super user. oh my god, really?? `createsuperuser` creates a super user?? I would've never guessed that. anyways, moving on....

Now that we  created a super user/admin, we can login to the admin page. if you go back to this url `http://127.0.0.1:8000/admin/` and login. you should see the admin page. 

Now, all you can see in the admin page is the `AUTHENTICATION AND AUTHORIZATION` app which was already created by `django`. Under this app, we have two models `User` and `Group`. The `User` model has all the users that registered in your website. So, if you go to the `Users`, you should see your user which is the super user that you just created.

But the question is why isn't the `Article` model that we just created here?
To have the `Article` model in the admin page, we'll use one of the files inside our `apps` folders. take a minute and go see the the structure of the `app` folder and try to take a guess. 

1 minute later...

And the answer is the `admin.py`.

In `main/admin.py`:
```python
from django.contrib import admin
from main import Article

admin.site.register(Article)
```

what `admin.site.register(Article)` does is basically register the `Article` model to the admin site. So, if we go back to the admin site, we'll see the `Article` model under the `main` app.
I now give you permission to go all crazy and add new articles, delete, change them, do whatever you want. you're a superuser, enjoy your privelages while they last.
