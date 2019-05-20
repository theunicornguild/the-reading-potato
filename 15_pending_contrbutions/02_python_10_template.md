`main/templates/contributions_list.html`
```html
{% extends "base.html" %}

{% block content %}
<ul>
	{% for contribution in contributions %}
		<li>
		    {{contribution.date}} - {{contribution.article}} - <a href="{% url 'contribution-details' contribution.id %}">Review</a>
	    </li>
	{% endfor %}
</ul>
{% endblock content%}
```

In the template we simply looped through the contributions and printed their information.

Do notice, that in the review button we're calling the `contribution-details` page which we still haven't created. That is the page where the author can see the changes that were made to the content and then decide to either accept or decline them.