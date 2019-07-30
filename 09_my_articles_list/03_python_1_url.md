`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('my-articles/', views.my_articles_list, name="my-articles-list"),
]
```

To get to the my articles page, the user has to enter this url in the browser `127.0.0.1/my-articles/`. This url would then call the `my_articles_list` view.


## Trello
> Move card `As a logged in user, I can see a list of my articles` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished my articles list functionality"
$ git push
```
___