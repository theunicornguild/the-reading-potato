Let's go back to what we were initially trying to do, which was creating a page where users can see a list of articles. 


## Trello
> Move card `As a user, I can see the list of articles` from the `Backlog` to the `Doing` list.
___

Each page that we create needs to have three things:
 * a `url` that points to this page or in our case, it would point to a `view`.
 * a `view` that will receive the user's request and returns a response.
 * a `template` which is the html page that the user will see.

#### View
Let's start with the `view`, A `view` takes a web request and does the necessary logic to return a web response. This response could be an html page, an image, or whatever the programmer decides to return. But, what we want to return here is an html page or what we would call a `template`.

This might come as a surprise to you but we write our `views` in the `views.py` file in our apps.

![tr](https://pbs.twimg.com/profile_images/977716002988417025/ty5cuTBr.jpg)

In `main/views.py`:
```python
from django.shortcuts import render

def articles_list(request):
    #whatever logic we need to write in our view
    return render(request, <TEMPLATE_NAME>)
```

This is our `view` and it's basically a function that I decided to call `articles_list`. This function is taking `request` as a parameter and at the end it's returning the `response`. These two things are what make a `view` a `view`, It takes a request and returns a response.

We'll start with what needs to happen  in the function/view.
Let's go one step back , what is the page supposed to show? a list of articles. 
So, our `template`/html page needs to show the list of articles. But where does the template get those articles from? the `view` is responsible for sending data to the `template` in the response.

Where does the `view` get the articles from?

Give it a thought before you actually scroll down to see the answer. Enjoy the dancing potato while you think.

![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

The answer is...drum roll please...
...
...
...
the `view` retrieves it from the database.

Since `models` are our connection to the database, we'll use them and do what we call a `query`. A `query` is basically a way for us to ask the database for certain objects. For example, we can ask the database for `all` `objects` under the model `Article` or `get` a specific `object` of the model `Article`.

In our case, we want `all` articles:
```python
Article.objects.all()
```

Let's add this to our view
```python
from django.shortcuts import render
from .models import Article

def articles_list(request):
    articles = Article.objects.all()
    return render(request, <TEMPLATE_NAME>)
```

Now our `view` is retrieving the articles from the database and then returning the `template` as the `response`. But these two are still not connected. the `template` haven't received anything from the view.

How does the `view` send data to the `temlpate`?
By creating a `dictionary` with data that needs to be sent to the `template` and then send that dictionary in the `render` function to be used by the `template`.

Let's see how that's done
```python
from django.shortcuts import render
from .models import Article

def articles_list(request):
    articles = Article.objects.all()
    context = {
        "articles" : articles,
    }
    return render(request, <TEMPLATE_NAME>, context)
```

The dictionay could be named anything, but it's a convention to call it `context`. Before we go to the template, let's give it a name, `articles_list.html`.

```python
def articles_list(request):
    articles = Article.objects.all()
    context = {
        "articles" : articles,
    }
    return render(request, "articles_list.html", context)
```