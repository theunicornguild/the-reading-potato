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

## Trello
> Move card `As a logged in user, I can edit my article's title and content` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished edit an article functionality"
$ git push
```
___