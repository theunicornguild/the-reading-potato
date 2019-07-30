`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('my-contributions/', views.my_contributions_list, name="my-contributions-list"),
]
```

Note: You can now add a link to `my-contributions-list` page in the navbar.

## Trello

> Move card `As a logged in user, i can see the status of the changes/contributions that I made to any article` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished my contributions list functionality"
$ git push
```
___
