The sent comparison result is now a list of strings, each string will either begin with `-`, `+`, ` `, or `?`. Here's what we want to do.
If the string begins with:
 * `+`: this means this is a new line added from the new_content. So, we'll highlights it with green.
 * `-`: this means this is a line that was in the current content but not in the new one. So, we'll highlight it with red.
 * ` `: this line exists in both contents. we'll leave it as it is.
 * `?`: lines starting with `?` will be ignored.

Let's see how we can do that
`main/templates/contribution_details.html`
```html
{% extends "base.html" %}

{% block content %}
    {% for line in comparison %}
    	{% if not line|make_list|first == '?' %}
    		{% if line|make_list|first == '-' %}
    			<p class="red-background">
    		{% elif line|make_list|first == '+' %}
    			<p class="green-background">
    		{% endif %}
    		{{line}}</p>
    	{% endif %}
    {% endfor %}
{% endblock content%}
```

Let's take this template line by line.

We looped through the lines
```html
{% for line in comparison %}
    ...
{% endfor %}
```

We're checking if the line starts with `?`. If it does, we'll just go to the next line in the array. 
`line` is the string, then we're converting it into a list of characters through `make_list`. Finally, we took the first character by using `first`. and checking if it equals `?`
```html
    {% if not line|make_list|first == '?' %}
        ...
    {% endif %}
```

If the first character is not `?`, we'll go to these lines. This checks whether the line starts with `-` or `+` and highlight them accordingly.
```html
		{% if line|make_list|first == '-' %}
			<p class="red-background">
		{% elif line|make_list|first == '+' %}
			<p class="green-background">
		{% else %}
		    <p>
		{% endif %}
		{{line}}</p>
```


The `green-background` and `red-background` are classes that I have written in a custom css file which we'll setup in the next part.