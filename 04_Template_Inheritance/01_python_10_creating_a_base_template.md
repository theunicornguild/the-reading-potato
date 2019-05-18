`template inheritance` is a way for us to decrease redundant code. we'll be doing that by creating a template with the things that are in common with all the pages and remove these redundancies from all the templates and instead make them `inherit` the code from the base template.

Let's start by creating a new template which will have everything the pages have in common. If you take a look at all the templates that we wrote, you'll find out that the below was written in all of them.

`main/templates/base.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    ....
</body>
```

These lines can be deleted from all the `templates` and inherit them from `base.html`. we can do that by creating blocks inside the template. A block is a reserved block that will be filled with html. Other `templates` that extend the `base.html` can specify the block they'd fill.

`main/templates/base.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    {% block content %}

    {% endblock content%}
</body>
```

`main/templates/article_details.html`
```html
{% extends "base.html" %}

{% block content %}
    <h1>{{article.title}}</h1>
    <h6>{{article.author}}</h6>
    <p>{{article.content}}</p>
{% endblock content%}
```

You can have as many blocks as you want in the base file and all you have to do in the templates is extend the base file and fill those blocks.

Take the time to extend the base file in all our templates and remove all the redundant code. Now, if you write anything in the `base.html` template, it will appear in all the pages that extend it.