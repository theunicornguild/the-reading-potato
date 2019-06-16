A css file is considered a `static` file. Static content is any content that can be delivered to an end user without having to be generated, modified, or processed.

Static files can be images, JS files, CSS files, and even fonts.

To setup static files to work properly we must go to our `settings.py` file and provide it with a `STATIC_URL` and a `STATIC_ROOT`.

Let's see what that looks like, then we'll go into what each one is for.
```python
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

Add the two lines above at the end of the `settings.py` file.

`STATIC_URL` is the URL pattern that you can use to access the static files and `STATIC_ROOT` is the path to where the static files are stored.

Next we need to actually use the `STATIC_URL` and `STATIC_ROOT` to dynamically create URLs to access any file with in a static directory.

Open up the `urls.py` file in the inner project folder and write the following lines of code, which specifies where project should look for the static files.

```python
...

from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    ...
]

urlpatterns+=static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

Any static file you want to keep in your project must be inside a static folder. You can have a static folder inside any of your Django apps.

Let's create a the `static` folder inside the app `main`. inside the `static` folder create a the css file. I'm naming is `colors.css`.

`main/static/colors.css`
```
.green-background {
	background-color: rgba(0,255,0,0.1);
}

.red-background {
	background-color: rgba(255,0,0,0.1);
}
```

note: If you want to add any static pictures such as a logo, it would also have to be saved in the `static` folder.

How would we actually use anything from our static folder? Well, in any HTML file you'd like to call static content into, you first have to load static then you can refer to any static file using the static tag.

Let's see what that looks like:
`main/templates/base.html`
```html
{% load static %}

<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <link rel="stylesheet" type="text/css" href="{% static 'colors.css' %}">
    </head>
```

We linked the css file in the `base.html` so that all pages will have access to it.
