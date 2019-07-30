#### Url

Finally, we just need to create a url path that the user can put in their browser to see the page that we created. We write the `urls` in a file called `urls.py`...try not to act too surprised.

open `reading_potato/urls.py`:
```python
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

By default, this is what you should have in your file. Try and take a minute to read the code and understand what's happening. try to focus on the `path`.

In the list `urlpatterns`, we can see one `path` which is the `admin/` which we've already used to get to the admin page where the url was `http://127.0.0.1:8000/admin/`. So, if we add another path `list/`, that means the user can access it like this `http://127.0.0.1:8000/list/` and so on.

Let's go through the cycle again.
 * The user enters the `url` in the browser.
 * The matching url calls its respective `view`.
 * The `view` return the response.
 * The user sees the response in his browser.

Let's create a path/url and specify a `view` for it.
```python
from django.urls import path
from main import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', views.articles_list, name="articles-list"),
]
```

If you go to this url `http://127.0.0.1:8000/articles/`, you should see your template `articles_list.html`. 

Let's try and explain what happened above in more detail. First, we imported the `views.py` file from the app `main`. Second, we created our path, we specified the url to be `articles/` and this url should call the `articles_list` view from the `views.py` file. Finally, the name attribute is just any name that you can give the path and you'll understand where the name comes in use later.

Now take some time to play around with the template, try to change the design, change the colours, choose the information you want to display and see how these changes reflect on your page.


## Trello
> Move card `As a user, I can see the list of articles` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished articles list functionality"
$ git push
```
___
