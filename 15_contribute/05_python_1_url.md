`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('contribute/<article_id>/', views.contribute_to_article, name="contribute-to-article"),
]
```

To access this page we can add a button in the article's detail that leads to this page.
`main/templates/article_details.html`
```html
...
{% if request.user == article.author %}
    <a href="{% url 'edit-article' article.id %}">Edit</a>
{% elif request.user.is_authenticated %}
        <a href="{% url 'contribute-to-article' article.id %}">Contribute</a>
{% endif %}
...
```
The author will see the `Edit` button while any other logged in user will see the `Contribute` button.


## Trello

> Move card `As a logged in user, I can contribute to any article's content and wait for approval` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished contributing functionality"
$ git push
```
___
