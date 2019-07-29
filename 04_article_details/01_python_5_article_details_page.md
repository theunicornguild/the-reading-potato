This page will have the articles details, basically all the information that we didn't show in the list. In this page we can show the content of the article, the author, who contributed, and just any information we want to show about this specific article. All article's will have the same details page, the only difference is the information shown on the page.

So, if it's only one page, then we need one `view`, one `url`, and one `template`.

___
## Trello
> Move card `As a user, I can see an articles details` from the `Backlog` to the `Doing` list.
___


Take some time to read the below code and try to make the connection between what's happening in the `view` ,`url` and `template`. The dancing potato is just under the code if you need to look at it while you think.

`main/views.py`
```python
def article_details(request, article_id):
    context = { "article" : Article.objects.get(id=article_id)}
    return render(request, 'article_details.html', context)
```
`reading_potato/urls.py`
```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', views.articles_list, name="articles-list"),
    path('articles/<int:article_id>/', views.article_details, name="article-details"),
]
```
`main/templates/article_details.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    ...
</body>
```
![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

Let's get into the details of what's happening:
In the `view`, we received two parameters, the `request` and another parameter called `article_id`. this parameter is sent from the url `articles/<int:articles_id>/`. Anything inside `<>` in a url means that this is a variable and whatever the name of this variable in the url is should be the same as the one sent as a parameter in the `view`. 

So, in the browser, you can use this url like this `http://127.0.0.1:8000/articles/1/`, `http://127.0.0.1:8000/articles/2/`, or just any number in the position of the variable. But, you need to understand that the sent value is going to be used by the `view`.So, `article_id` will hold the value `1` when this `url` is used `http://127.0.0.1:8000/articles/1/`. 

If we go back to the view and see this line `Article.objects.get(id=article_id)`, we're retrieving one article from the database using the `get` query. So, we're getting the article that has the id equal to the number that was sent through the url.

For example, this url `http://127.0.0.1:8000/articles/1/` will retrive this article from the database `Article.objects.get(id=1)`.

Note: `get` is used when you know the query will return only one object. If the query does not return an object or return more than one, it will throw an error.

All that's left now is to write something real in our template. 
`main/templates/article_details.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    <h1>{{article.title}}</h1>
    <h6>{{article.author}}</h6>
    <p>{{article.content}}</p>
</body>
```