This is the page where you'll be able to see all the contributions made to your articles that are awaiting your approval.

## Trello
> Move card `As a logged in user, I can see a list of my articles that people contributed in and need my review` from the `Backlog` to the `Doing` list.
___


`main/views.py`
```python
def contributions_list(request):
	if request.user.is_anonymous:
		return redirect('articles-list')

	contributions = Contribution.objects.filter(status=Contribution.PENDING, article__author=request.user)
	context = {"contributions" : contributions}
	return render(request, 'contributions_list.html', context)
```

This `view` starts by checking permissions, and then retrievs the contributions and sends them through the context to the `template`.

Let's take a look at how the `Contributions` where filtered out
```python
contributions = Contribution.objects.filter(status=Contribution.PENDING, article__author=request.user)
```
First, we've got the `status` which should equal `Pending`, the variable `PENDING` in the `Contribution` model was used (go back to the model and take a look). This was done instead of actually writing `status = "Pending"` was just to make sure no human errors such as misspelling `Pending`.

Next, we were able to filter according to the `author` of the `article` (where `article` is a field in the `Contribution` model) by using `__`(double underscore) which allows us to get the value of one of the article's fields.