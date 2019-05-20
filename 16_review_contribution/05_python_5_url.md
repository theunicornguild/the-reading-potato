`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('contributions/<int:contribution_id>/', views.contribution_details, name="contribution-details"),
]
```