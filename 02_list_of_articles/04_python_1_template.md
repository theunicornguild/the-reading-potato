#### Template

Next, we'll create the template, we only have a name for it so far, but the actual `template` still haven't been created. 

In django, when we specify a `template`'s name, it searches for it inside the `app` inside a folder called `templates`. So, start by creating that folder and then inside it create the `html` file.

`main/templates/articles_list.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>

</head>
<body>
</body>
```

I will repeat this again. all templates/html pages need to be inside a folder called `templates` in the app.
**NOT** `template`
**NOT** `Templates`
**NOT** anything else
it has to be called `templates`

Going back to `articles_list.html`, any html that we write in this page will be shown to the user as the response from the view. What we want the user to see is the list of articles. We sent the list of articles to the `template` through the context dictionary. So, we'll use that dictionary to show the information  in the html.

###### How to access the information sent through the dictionary:
 * use the keys in the dictionary to get the value.
 * use the key inside double curly brackets `{{<KEY>}}`.
 * use the dot notation to get information inside your object using the field's names. Ex:`{{<KEY>.title}}`

If we wanted to show the whole list of `Articles` in our template, we'd write `{{articles}}`.
If we wanted to show the first `Article` in the list we write `{{articles.0}}`.
If we wanted to show the title of the first item in the list, we write `{{articles.0.title}}`.

Obviously, we won't call each article in the list, usually with lists we use `for` loops and that's what we're going to use in this `template`. Django provides us with special tags that we can use in the templates and one of them is the `for` tag. All tags look like this `{% <SOMETHING_HERE> %}`. The for loop would look like this `{% for <VARIABLE_NAME> in <LIST> %}`.

`main/templates/articles_list.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    <ul>
        {% for article in articles %}
            <li>
                <h1>{{article.title}}</h1>
                <p>{{article.created_on}}</p>
            </li>
        {% endfor %}
    </ul>
</body>
```

let's take this step by step.
 1. An unordered list was created `<ul>`.
 2. Inside the list we looped through the articles, where the `articles` is the key used in the `context` dictionary sent by the `view`.
 3. For each `article` from our list of `articles`, we created a list item `<li>`.
 4. Inside of the list item, we used the variable `article` variable to get the information inside it.
