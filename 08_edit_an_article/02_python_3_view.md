Now that users are able to create articles, they should also be able to edit them afterwards. Again, this will need a form. However, we need to decide on what the user is allowed to edit.

Can they edit the content?

Can they change the title or is it set?

So, depending on the decisions that we make, we create the form. 

I've decided to let the user edit both the title and content. That means the form  will have both `title` and `content` in its fields. We've already created such a form (`ArticleForm`) so we'll use that.

##### view

```python
def edit_article(request, article_id):
	article = Article.objects.get(id=article_id)

	form = ArticleForm(instance=article)
	if request.method == "POST":
		form = ArticleForm(request.POST, instance=article)

		if form.is_valid():
		    form.save()
			return redirect('article-details', article_id)

	context = {"form":form, "article":article}
	return render(request, 'edit_article.html', context)
```

This is very similar to creating an article. The only difference is that this article already exists and we're only updating it. So, we first need to retrieve it from the database.

Then, we need to fill the form with article's data. Because, when the user opens the edit page, they don't want to see an empty form. They want the form with the title and content and then they could erase or change whatever they want. 

That is how the form was filled
```python
form = ArticleForm(instance=article)
```

Do note that this time we saved the article to the database directly because there was nothing that we needed to set.
```python
form.save()
```
We've also sent the article in the context to be used in the `template` when the form is submitted.

After that everything else is just like the create.
