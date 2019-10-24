`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('contributions/', views.contributions_list, name="contributions-list"),
]
```

Note: You can now add a link to `contributions-list` page in the navbar.
