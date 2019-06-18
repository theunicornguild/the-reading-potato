To provide users with a better user experience, we can add a search bar to find a specific article that they're looking for.

This is how a search bar looks like
```html
    <form action="#" class="form-inline">
        <input class="form-control" type="search" placeholder="Search" aria-label="Search">
        <button class="btn" type="submit">Search</button>
    </form>
```

For this form to work there are several things we need to specify:
 * when the form is submitted, which view should we make a request for.
 * what is the request method? is it a get or a post?
 * specify the name of the input so we can retrieve it in the view

#### Which view should we make a request for?
Since this is a search bar for articles, then it would make sense that when the form is submitted we should go to the `articles-list` page to see the filtered list of articles.
```html
	<form action="{% url 'articles-list' %}" class="form-inline">
		...
	</form>
```

#### What is the request method?
We're not sending a big amount of data, nor are we sending information we don't want the user to see in the url. So, it'll be a `GET` request.
```html
	<form action="{% url 'articles-list' %}" class="form-inline" method="GET">
		...
	</form>
```

#### Input name
We can give the input any name we want. But, whatever name we use here has to be the same name we'll be using in the `articles_list` view.
```html
		<input class="form-control" type="search" placeholder="Search" aria-label="Search" name="q">
```

What a `GET` request does is send the information through the url using the specified name. So, in our case, if we wanted to search for an article that has the word `potato` in it, the url would be like so `127.0.0.1/articles/?q=potato`. Where q is the name we specified and potato is the value that will be sent to the view.

Try this out. Go to `google.com/?q=<ANYTHING>`. Put any value for `q` and see what happens.

Now we need to decide where want to put this form. In my case, I want to add it to the navbar.
`main/templates/base.html`
```html
...
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="{% url 'articls-list' %}">The Reading Potato</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
            <div class="navbar-nav">
                {% if request.user.is_authenticated %}
                    <a class="nav-link" href="{% url 'create-article' %}">Create</a>
                    <a class="nav-link" href="{% url 'my-articles-list' %}">My Articles</a>
                    <a class="nav-link" href="{% url 'contributions-list' %}">Contributions</a>
                    <a class="nav-link" href="{% url 'my-contributions-list' %}">My Contributions</a>
                    <a class="nav-link" href="{% url 'logout' %}">Logout</a>
                {% else %}
                    <a class="nav-link" href="{% url 'login' %}">Login</a>
                    <a class="nav-link" href="{% url 'register' %}">Register</a>
                {% endif %}
            </div>

        <form action="{% url 'articles-list' %}" class="form-inline" method="GET">
			<input class="form-control" type="search" placeholder="Search" aria-label="Search" name="q">
			<button class="btn" type="submit">Search</button>
		</form>
      </div>
    </nav>
...
```

If you try the search bar, you'll notice that it isn't really functional. It takes you to the `articles-list` page, but the articles aren't really filtered. 

Just because we called it a search bar does not mean it will magically start searching and filtering. We need to do that in the view.

The list view needs to handle the GET request that it's receiving when someone is trying to search for something.

Let's take a look at what our list view currently looks like.
`main/views.py`
```python
def articles_list(request):
    articles = Article.objects.all()
    context = {
        "articles" : articles,
    }
    return render(request, "articles_list.html", context)
```

Currently it's just retrieving all the objects and passing them to the context dictionary to be rendered in the HTML page.

We need to filter the list based on what the user is typing into the search bar and then pass it to the context dictionary. Let's see how we can do that.
`main/views.py`
```python

    
def articles_list(request):
    articles = Article.objects.all()

    query = request.GET.get("q")
    if query:
        articles = articles.filter(title__contains=query)

    context = {
        "articles" : articles,
    }
    return render(request, "articles_list.html", context)
```

We're retrieving from the `GET` request the value of the parameter called `q` using the `get` function. The `GET` parameter is called `q` because that's what we named the text input in the form for the search bar.

The value of `q` represents what was typed in the search bar and submitted. We save that value into the variable called `query`.

We then check if `query` exists, because your users will not always be searching for something when accessing the list view. As a user I can view the list page without searching can't I?

If `query` exists, we use the `filter` QuerySet to filter the article objects using the `title` field. You can only use fields from the model you are querying.

`title__contains=query` means whatever I searched for is inside of the title value. For example, I searched for **apple** and there is a article with the title **Pineapple**. **Pineapple** has the word **apple** in it, so it will be within the QuerySet. 

There are situations were we would like the search functionality to overlook the letter case. For case insensitive lookups we can use `icontains`, for example `title__icontains=query` will still return Pineapple if I searched for APPLE.

Notice that double underscores( \_\_ ) are used for [Field Lookups](https://docs.djangoproject.com/en/dev/topics/db/queries/#field-lookups), Which iterates through the dictionary created using python keyword arguments, these keyword arguments are QuerySet methods taking the general form of `field__lookuptype`.


#### Extra Trick

You might have noticed something. Every time you type something into the search bar and click enter to submit your search query, your search query disappears from the search bar.

What if you want to keep it there? Maybe you want to make minor adjustments for your next search.
```html
<form action="{% url 'articles-list' %}" class="form-inline" method="GET">
	<input class="form-control" type="search" placeholder="Search" aria-label="Search" name="q" value="{{request.GET.q}}">
	<button class="btn" type="submit">Search</button>
</form>
```

We used a GET method for the form, so when we submit the form the parameter values are available in the URL.

The value attribute of the text input was set to {{request.GET.q}}.

{{request.GET.q}} retrieves the value for q from the GET parameters that are available in the URL, from the request that was just submitted.




