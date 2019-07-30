One more thing about permissions, it doesn't stop at whether the user is logged in or not. a good example for the reading potato would be editing an article. We should only allow the author to edit and the edit button should only be visible to the author of the article.

Let's go back to the `edit_article` view
`main/views.py`
```python
def edit_article(request, article_id):
    article = Article.objects.get(id=article_id)
    
    if article.author != request.user:
        return redirect('article-details', article_id)
        
    ...
    
    return render(request, 'edit_article.html', context)
```

What we did was we checked if the user that made the request is **not** the author of the retrieved article, then we redirected him to the articles details page without giving him access to the edit page.

Next, let's make the button only visible to the author
`main/templates/article_details.html`
```html
...
{% if request.user == article.author %}
    <a href="{% url 'edit-article' article.id %}">Edit</a>
{% endif %}
...
````

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "added permissions"
$ git push
```
___