`authentication/templates/login.html`

```html
{% extends "base.html" %}
{% load crispy_forms_tags %}

{% block content %}
    <form action="{% url 'login' %}" method="POST">
	    {% csrf_token %}
	    {{form|crispy}}
	    <input type="submit" value="Login">
	</form>
{% endblock content%}
```

___
## Trello
> Move card `As a user, I can login using my username and password` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___