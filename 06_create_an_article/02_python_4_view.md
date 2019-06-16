Now that the form is ready, we can start creating the page for creating an article. To create a page we need three things:
 * `view`
 * `template`
 * `url`

let's start with the `view`

###### view 

`main/views.py`
```python
from .forms import ArticleForm
from .models import Artcle
...

def create_article(request):
	form = ArticleForm()
	if request.method == "POST":
		form = ArticleForm(request.POST)
		if form.is_valid():
			article = form.save(commit=False)
			article.author = request.user
			article.save()
			return redirect('article-details', article.id)

	context = {"form" : form}

	return render(request, "create_article.html", context)
...
```

In this view, two things can happen, either the user is just requesting to see the page with an empty form OR the user filled the form and now he's submitting it. When a user submits a form that's a `post` request since the user is sending data in the request.

In this line an empty form is created, `form` is just a variable name, it could be anything.
```python 
form = ArticleForm()
```

Then this form is sent through the context to the template.
```python
context = {"form" : form}

return render(request, "create_article.html", context)
```
If the request method was `POST` which means the user entered data in the form and is now submitting it. we'll create a new form but this time we'll fill it with the received data
```python 
form = ArticleForm(request.POST)
```

Now all we have is a form filled with data. The next thing that happens is we check if the data sent was valid. For example, if a field is required, it checks that it was not left empty or if the field only accepts numbers, it checks for that and so on.
```python
    ...
		if form.is_valid():
		    ...
```

After we checked for the forms validity and we know that the information sent by the user is valid, we can now save the article. Since the `ArticleForm` is a `ModelForm`, all we have to do is `form.save()` and the information received in the form will be used to create an `Article` object and save it to the database.

In our case, we don't want to save the `Article` to the database yet because there is one more thing that we need to do. The form has the `title` and the `content` but it is our job to set the `author`. So we did this:
```python
article = form.save(commit=False)
article.author = request.user
article.save()
```

what this does is it creates an `Article` object without saving it into the database. So, `article` is now an `Article` object. 
```python
article = form.save(commit=False)
```
Then we manually set the author as the person who made the request. We can get the logged in user from the `request` variable that is received as a parameter in every view. Finally, we save it to the database.
```python
article.author = request.user
article.save()
```