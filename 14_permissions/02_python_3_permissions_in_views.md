Before we start with adding permissions we need to decide what happens what happens if a user that shouldn't access a `view` accesses it. 


Let's say an `anonymous` user has the url to the `create-article` page, and he opens it in his browser. The page will open unless we do something about it because we're a silent guardian, a watchful protector, a Dark Knight.

![batman](https://media.giphy.com/media/6gDSyjaOPwZ4A/giphy.gif)

As a silent guradian, I would say(that wouldn't make me silent anymore though) that if an `anonymous` user requests a page for only `authenticated` users, it would make sense to redirect them to the login page.

Let's see how that's done
`main/views.py`
```python
def create_article(request):
    if request.user.is_anonymous:
    	return redirect('login')
    		
    ...

    return render(request, "create_article.html", context)
```

Here we're checking if the user is not logged in, using the `is_anonymous` attribute. In the scenario that this is `True`, it'll redirect the user to the login view. With this we've secured our `create_article` view.

Let's have another example for the opposite scenario. An `authenticated` user is trying to access the `login_view`. 

`main/views.py`
```python
def login_view(request):
    if request.user.is_authenticated:
        return redirect('articles-list')
       
    ...
    
    return render(request, 'login.html', context)
```

In this case if a logged in user is accessing this view, they'll be redirected to the `articles-list` page.

Before adding permissions to the `templates`, it's your task to secure the rest of the views. Enjoy.

![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

After that dance you should be done with the views. So, we'll move on to the `templates`.
