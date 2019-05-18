When we add anything in any website, like adding a new address to your account or registering which is basically creating a new user, in all those cases we are filling a form. The form has several fields, some are required, some are optional, and at the end we press a button to submit this form which will lead to creating an object for whatever we we're filling the form for.

Therefore, For us to create an article we need to create a form. This form will have fields for the user to fill out. If we took a step back and saw our `Article` model we'd know what fileds we have. 
* `title`: the user should be able to write his own title.
* `content`: the same thing goes for the content.
* `author`: the user shouldn't be able to enter who the author is. our website should be smart enough to know who is creating this article.
* `created_on` and `last_update`: are set automatically.

From the above we know two things:
 * the `title` and the `content` should be present in the form shown to the user.
 * we need to set the `author` automatically.

Let's start with the form. This is how a form with just title and content would look like. And in the `view`, we would need to extract the information from the form, then use this information to create a new `Article` object.
```html
<form>
    <label>Title</label>
    <input type="text" name="title">
    
    <label>Content</label>
    <textarea type="text" name="content"></textarea>
    
    <input type="submit" value="Create">
</form>
```

Imagine if the form had even more fields and not just text inputs. things would start getting even more complicated. Fortunately, django provides us with a way to create `forms` in a much easier way by using the `forms` library. It allows us to create the structure of the form as a `class`. Then, everytime we create a new instance of that class, we get a new empty form with the specified structure.

Create a new file in our `main` app called `forms.py`

`main/forms.py`
```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
	class Meta:
		model = Article
		fields = ['title', 'content']
```

we're creating a form called `ArticleForm`. This form is connected to a model that's why it inherits from `ModelForm`. The model it's connected to is the `Article` model. From that model, we want the `title` and `content` fields to be added to the form.

Take a minute, go back to the `Article` model and let everything sink in.
![sink](https://media.giphy.com/media/13PZ0dKw1J3LzO/giphy.gif)