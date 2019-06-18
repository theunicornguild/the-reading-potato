`reading_potato/urls.py`
```python
...
from main import views
from authentication import views as auth_views

urlpatterns = [
    ...
    path('login/', auth_views.login_view , name="login"),
]
```



