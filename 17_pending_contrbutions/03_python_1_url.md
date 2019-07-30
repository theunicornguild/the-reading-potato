`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('contributions/', views.contributions_list, name="contributions-list"),
]
```

Note: You can now add a link to `contributions-list` page in the navbar.

## Trello

> Move card `As a logged in user, I can see a list of my articles that people contributed in and need my review` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished list contributions that are awaiting user's approval functionality"
$ git push
```
___