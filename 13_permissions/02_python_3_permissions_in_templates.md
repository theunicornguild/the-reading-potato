`main/templates/base.html`
```html
...
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="{% url 'articls-list' %}">The Reading Potato</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
        {% if request.user.is_authenticated %}
            <a class="nav-link" href="{% url 'create-article' %}">Create</a>
            <a class="nav-link" href="{% url 'my-articles-list' %}">My Articles</a>
            <a class="nav-link" href="{% url 'logout' %}">Logout</a>
        {% else %}
            <a class="nav-link" href="{% url 'login' %}">Login</a>
            <a class="nav-link" href="{% url 'register' %}">Register</a>
        {% endif %}
        </div>
      </div>
    </nav>
...
```

Let's break this down

```html
{% if request.user.is_authenticated %}
```

What we did here was check, if the user `is_authenticated`, then show the below links
```html
<a class="nav-link" href="{% url 'create-article' %}">Create</a>
<a class="nav-link" href="{% url 'my-articles-list' %}">My Articles</a>
<a class="nav-link" href="{% url 'logoutr' %}">Logout</a>
```
else, these would show
```html
<a class="nav-link" href="{% url 'login' %}">Login</a>
<a class="nav-link" href="{% url 'register' %}">Register</a>
```