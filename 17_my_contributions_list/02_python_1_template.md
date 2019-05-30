`main/templates/my_contributions_list.html`
```html
{% extends "base.html" %}

{% block content %}
<table class="table">
	<thead>
	    <tr>
	    	<th scope="col">Status</th>
	      	<th scope="col">Article</th>
	      	<th scope="col"></th>
	    </tr>
	</thead>
	<tbody>
		{% for contribution in request.user.contributions.all %}
		    <tr>
			    <td>
			    	{{contribution.status}}
				</td>
			    <td>{{contribution.article}}</td>
			    <td>
			      	{{contribution.date}}
		  		</td>
		    </tr>
		{% endfor %}
	</tbody>
</table>
{% endblock content %}
```

We were able to loop through the contributions by getting the user from the request. Then, we got `all` the contributions related to the user by using the `related_name` that was set in the `Contribution` model for the user field.
```html
{% for contribution in request.user.contributions.all %}
```