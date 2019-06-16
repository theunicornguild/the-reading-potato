We can register and login, But we still can't logout. For each functionality, we always had a `view`, `template`, and a `url`. 

The `view` was for doing the actual action like the login in, creating the user for registrarion or retrieving data from the database. 

The `url` was to make a request which leads to accessing this `view`.

Finally, the `template` displayed the information we wanted the user to see.

But, for logging out do we need all these three. Let's think about it.

![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

We need the `view` to make the actual action of clearing the user from the session which is logging out.
We need the `url` to make a request and access this view.
But, we don't really need a `template`, because logging out does not need a page to be displayed for the user. It will only be a button that can be in any page. This button triggers the logging out action and that's it. There isn't something to be seen.

##### view
Let's start with the `view`. This view might seem confusing at first but if you give it enough time and let it sink in, it will start making sense.

`authentication/views.py`
```python
...
from django.shortcuts import render, redirect
from django.contrib.auth import login, authenticate, logout

...
def logout_view(request):
	logout(request)
	return redirect('articles-list')
...
```

This view uses the `logout` function which takes the request and deletes the session history for that request. Which leads to logging out the user.

Then the user is redirected to the `articles-list` page.

##### url
`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('logout/', auth_views.logout_view, name="logout"),
]
```