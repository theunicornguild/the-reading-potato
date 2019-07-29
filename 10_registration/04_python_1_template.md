The `template` for the register page will also be saved in the `authentication` app. For any `template` that we want to create we have to save it inside of the `templates` folder in an app because this is where django searches for the `templates`.

Create a folder called `templates` in the `authentication` app.



`authentication/templates/register.html`

```html
{% extends "base.html" %}
{% load crispy_forms_tags %}

{% block content %}
    <form action="{% url 'register' %}" method="POST">
	    {% csrf_token %}
	    {{form|crispy}}
	    <input type="submit" value="Register">
	</form>
{% endblock content%}
```

The only difference in this template from the `article_create.html` is the `action` url.

___
## Trello
> Move card `As a user, I can register with a username, email, first and last name, and password` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___