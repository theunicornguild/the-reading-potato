`main/views.py`
```python
...
from .forms import ArticleForm, ContributeArticleForm
from .models import Article, Contribution, Change

def contribute_to_article(request, article_id):
	if request.user.is_anonymous:
		return redirect('login')
		
	article = Article.objects.get(id=article_id)
	
	#the author shouldn't be able to contribute, they can only edit
	if article.author == request.user:
		return redirect('edit-article', article_id)

	form = ContributeArticleForm(instance=article)
	if request.method == "POST":
		form = ContributeArticleForm(request.POST)

		if form.is_valid():
			changed_article = form.save(commit=False)
			contribution = Contribution.objects.create(user=request.user, article=article)
			Change.objects.create(new_content=changed_article.content, contribution=contribution)
			return redirect('my-contributions-list')

	context = {"form":form, "article":article}
	return render(request, 'contribute_to_article.html', context)
```

We started this `view` with permissions:
 * only logged in users can access this `view`
 * the author of the article cannot contribute but can directly edit the article.

Next we go to the actual work, if it's a `get` request, a form with the article's content is shown to the user.

In case of a `post` request which means the user is submitting his contribution, we'll need to get the new content. That was done by saving the article into a variable without saving it to the database through using `commit = False`.
```python
changed_article = form.save(commit=False)
```
Next, we create the contribution object
```python
contribution = Contribution.objects.create(user=request.user, article=article)
```
Now, we have the contribution object, which specifies who made the contribution and to which article. However, the new content is still not saved and that's done through the `Change` model.
```python
Change.objects.create(new_content=changed_article.content, contribution=contribution)
```
The change object was created by setting the new content and connecting it to the created contribution.

Note that status of the contribution is `Pending` by default.



