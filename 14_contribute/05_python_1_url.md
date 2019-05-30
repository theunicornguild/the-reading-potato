`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('contribute/<article_id>/', views.contribute_to_article, name="contribute-to-article"),
]
```

To access this page we can add a button in the articles detail that leads to this page.
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