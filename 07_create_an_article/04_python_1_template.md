`main/templates/create_article.html`

```html
{% extends "base.html" %}

{% block content %}
    <form action="{% url 'create-article' %}" method="POST">
	    {% csrf_token %}
	    {{form}}
	    <input type="submit" value="Create">
	</form>
{% endblock content%}
```

There are three things you need to notice in this template:
 * `method="POST"`: we specified the forms method as `post`.
 * `{% csrf_token %}` is a form of security for submitting the form.
 * `action`: when the form is submitted the action is to call the `create-article` url.

Note: for this to work, the user needs to be logged in so that they can be set as the author. So, in order to try this page out, sign in in the admin page first.

Since bootstrap is already set in the `base.html`, I'll leave the styling for you to do. However, since this is our first time going through forms, I'll show you a little trick to style forms seamlessly using `crispy forms`.

`Crispy forms` is a Django package that allows you to style your forms in a very elegant and DRY way. It takes very minimal effort to set up and apply.

We'll have to start by installing the package using pip. But first, go to your terminal and make sure you're in your project directory with your virtual environment activated.
```
(env)$ pip install django-crispy-forms
```

After installing crispy forms, go to your `settings.py` file inside your inner project folder and add `crispy_forms` to your `INSTALLED_APPS` list.
```python
INSTALLED_APPS = [
    ...
    'crispy_forms',
]
```
Finally under `INSTALLED_APPS` add the following line of code.
```python
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```
Here we provided crispy forms with the styling toolkit that we're using. Since we use Bootstrap, we provided it with the latest version of Bootstrap, which is Bootstrap4.

Using crispy forms is very simple. You go to the template that has a form and load the crispy template tags. Then you just apply it to the form element.

Let's see how this is done.
```html
{% extends "base.html" %}
{% load crispy_forms_tags %}

{% block content %}
    <form action="{% url 'create-article' %}" method="POST">
        {% csrf_token %}
        {{form|crispy}}
        <input type="submit" value="Create">
    </form>
{% endblock content%}
```
`{% load crispy_forms_tags %}` was used in the beginning of the file to load the template filter provided by crispy forms. Then we used the crispy template filter to make the form crispy (`{{form|crispy}}`).

And just like that our form is styled

![mind blown](https://media.giphy.com/media/xT0xeJpnrWC4XWblEk/giphy.gif)


## Trello
> Move card `As a logged in user, I can add a new article` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___


### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished creating an article functionality"
$ git push
```
___
