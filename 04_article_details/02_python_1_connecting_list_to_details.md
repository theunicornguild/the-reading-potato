Now that we have two different pages (the list and details), let's try and connect them. So, if you click on an article in the list, it should take you to the details of this article. 

To do this we need to know one thing. the url that takes to the details page. This is how it's defined in `urls.py`.
```python
path('articles/<int:article_id>/', views.article_details, name="article-details")
```
Then in the template, we'll use the `url` tag which takes the name of the url and any parameters the url takes which in this case is `article_id`. The url tag then takes the url name and whatever parameters were passed and converts it to the `path`/`url` that has the received name.

In `main/templates/articles_list.html`, we'll specify that when the title is clicked, take me to its details.
```html
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    <ul>
        {% for article in articles %}
            <li>
                <a href="{% url 'article-details' article.id %}">
                    <h1>{{article.title}}</h1>
                </a>
                <p>{{article.created_on}}</p>
            </li>
        {% endfor %}
    </ul>
</body>
```

___
## Trello
> Move card `As a user, I can see an articles details` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished article details functionality"
$ git push
```
___
