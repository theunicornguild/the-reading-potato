`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('edit/<int:article_id>', views.edit_article, name="edit-article"),
]
```

To get to the edit page, the user has to enter this url in the browser `127.0.0.1/edit/<ID>/`. This url would then call the `edit_article` view. So, if the user wants to edit the article with `id=1`, the url would be `127.0.0.1/edit/1/`.

You can add a button in the article details page to take us to the edit page like so
```html
<a href="{% url 'edit-article' article.id %}">Edit</a>
```
