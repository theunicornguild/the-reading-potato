`reading_potato/urls.py`
```python
from django.contrib import admin
from django.urls import path
from main import views

...
urlpatterns = [
    ...
    path('create/', views.create_article, name="create-article"),
]
```

To get to the create page, the user has to enter this url in the browser `127.0.0.1/create/`. This url would then call the `create_article` view. 

Keep in mind that all views were imported from the app `main`
```python
from main import views
```