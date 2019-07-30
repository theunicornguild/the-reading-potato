`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('contributions/<int:contribution_id>/', views.contribution_details, name="contribution-details"),
]
```

## Trello

> Move card `As a logged in user, I can review changes/contributions made to my articles` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished review contribution functionality"
$ git push
```
___