`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('my-contributions/', views.my_contributions_list, name="my-contributions-list"),
]
```

Note: You can now add a link to `my-contributions-list` page in the navbar.