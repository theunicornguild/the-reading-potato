`main/templates/contribute_to_article.html`
```html
{% extends "base.html" %}
{% load crispy_forms_tags %}

{% block content %}
    <form action="{% url 'contribute-to-article' article.id %}" method="POST">
        {% csrf_token %}
        {{form|crispy}}
        <input type="submit" value="Contribute">
    </form>
{% endblock content%}
```