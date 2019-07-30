Before we can write the url for the registration page, we need to import the views from the `authentication` app. Since in `reading_potato/urls.py`, we've only imported the views from the `main` app.
```python
from main import views
```

So, all we have to do is import them just like we did for the `main` app.
```python
from main import views
from authentication import views
```

However, what we just did may cause problems. Because we've imported `views` from both apps. Now they're two different files but have the exact same name. 

This is the best way to explain it.

![same same](https://media.giphy.com/media/C6JQPEUsZUyVq/giphy.gif)



So, if we did this, how does it know that the `views` is the one imported from `authentication` and not `main`. The same goes for all the other paths that are using the `views` from the `main` app. How does it know that the `views` is the one imported from `main` and not `authentication`. 

To solve this we need a way to differentiate between them. All we're going to do is give one of the `views` an alias or you could say a nickname. Just like if you have two friends with the same name. If you call one of them, both of them will turn. But, if each friend has a nickname and you call them by that nickname then all problems are solved.

So, I'll give an alias `auth_views` to the `authentication` views and we'll use the `auth_views` to get the `register` view.


`reading_potato/urls.py`
```python
...
from main import views
from authentication import views as auth_views

urlpatterns = [
    ...
    path('register/', auth_views.register, name="register"),
]
```