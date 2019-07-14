`main/templates/my_articles_list.html`
```html
{% extends "base.html" %}

{% block content %}
    {% for article in user.articles.all %}
    	<a href="{% url 'article-details' article.id %}">
    		<h1>{{ article.title }}</h1>
    	</a>
    	<hr>
    {% endfor %}
{% endblock content %}
```

we used the `user` which is the logged in user that made the request. Then, using the `related_name` option we can get the `articles` that are connected to this user through the `ForeignKey` relationship. Finally, we specified `all` to get all the articles that belong to this user.

So, if there is any information that you can get from the `user` one way or another, there is no need to send it or retrive it in the view.