As the number of articles increases in our website, we need a better way to view them. Rather than having all the articles show up at once and the user would have to scroll down forever, it's better if separate them into pages. Just like when you google something, not all results are shown in one page, you'd have to click next to see the results of the 2nd page and so on. 

This is called `pagination`. So, we'll apply `pagination` to the articles list page.

`main/views.py`
```python
...
from django.core.paginator import Paginator, EmptyPage, PageNotAnInteger
...


def articles_list(request):
    articles = Article.objects.all()

    query = request.GET.get("q")
    if query:
        articles = articles.filter(title__contains=query)

    paginator = Paginator(articles, 10) # Show 10 articles per page
	page_number = request.GET.get('page')

	try:
		objects = paginator.page(page_number)
	except PageNotAnInteger:
		# If page is not an integer, deliver first page.
		objects = paginator.page(1)
	except EmptyPage:
		# If page is out of range (e.g. 9999), deliver last page of results.
		objects = paginator.page(paginator.num_pages)

    context = {
        "articles" : objects,
    }
    return render(request, "articles_list.html", context)

...


```

We first needed to import a few things so we can use the `Django Paginator`. The first thing that we did was we gave `Paginator` our `articles` and the number of articles we’d like to have on each page, and that gives us methods for accessing the items for each page. 
```python
paginator = Paginator(articles, 10)
```

Then, we retrieve the page the user is trying to access and this falls under three scenarios:

1. User access a valid page and we get the page items and save them to a list called `objects`.
2. User inputs invalid values (not integer), so he will be redirected to the content of page 1.
3. User inputs a page number that does not exist so he is redirected to the last page.
```python
	page_number = request.GET.get('page')

	try:
		objects = paginator.page(page_number)
	except PageNotAnInteger:
		# If page is not an integer, deliver first page.
		objects = paginator.page(1)
	except EmptyPage:
		# If page is out of range (e.g. 9999), deliver last page of results.
		objects = paginator.page(paginator.num_pages)
```

When the articles are saved in the `objects` list from whichever scenario the user falls under, we pass the `objects` list into the context data now instead of the `articles` list.

You're seeing something a little new here when we're dealing with the scenarios, `try` and `except`. Basically what's happening is, it will try to go through the `try` scenario and if something goes wrong, it will go under one of the `exceptions` depending on what happened.


 We'll have to add some code in our `articles_list.html` so that we can switch between pages and make the requests. You can add this code anywhere you want the pagination to be.

 `main/templates/articles_list.html`

```html
...

<div class="pagination">
    <span class="step-links">
        {% if articles.has_previous %}
            <a href="?page={{ articles.previous_page_number }}"><</a>
        {% endif %}

        <span class="current">
             {{ articles.number }} of {{ articles.paginator.num_pages }}
        </span>

        {% if articles.has_next %}
            <a href="?page={{ articles.next_page_number }}">></a>
        {% endif %}
    </span>
</div>

...
```

We basically added this `pagination` `div` at the bottom of our code. This block of code does a couple of things:

1. Checks if there's a next page, if so it provides you a link to it.
2. Checks if there's a previous page, if so it provides you a link to it.
3. Displays which page you're on and how many pages there are in total.

Go and test it now on your browser.

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "added pagination"
$ git push
```
___