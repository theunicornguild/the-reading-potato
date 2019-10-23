`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('my-articles/', views.my_articles_list, name="my-articles-list"),
]
```

To get to the my articles page, the user has to enter this url in the browser `127.0.0.1/my-articles/`. This url would then call the `my_articles_list` view.
