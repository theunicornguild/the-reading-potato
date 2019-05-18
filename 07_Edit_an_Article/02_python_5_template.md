`main/templates/edit_article.html`
```html
{% extends "base.html" %}
{% load crispy_forms_tags %}

{% block content %}
    <form action="{% url 'edit-article' article.id %}" method="POST">
        {% csrf_token %}
        {{form|crispy}}
        <input type="submit" value="Edit">
    </form>
{% endblock content%}
```

Do notice that when the form is submitted, we had to give the `article_id` to the url because it's used in the view to retrieve the article. Otherwise, it wouldn't know which article to update.