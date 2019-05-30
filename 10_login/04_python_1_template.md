`authentication/templates/register.html`

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