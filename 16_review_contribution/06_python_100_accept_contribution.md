Accepting a Contribution does not require a `template` since there is not a page to be seen after you accept a contribution. So, we will only be needing a `view` and a `url` to that `view`.

What happens when the contribution is accepted?
 * the contributions status is changed to accepted
 * the articles content is changed to the new content
 * the `Change` object conncted to this contribution is deleted

Let's see how that's done

##### view
```python
def accept_changes(request, contribution_id):
	contribution = Contribution.objects.get(id=contribution_id)

	if request.user != contribution.article.author:
		return redirect('articles-list')

	
	contribution.status = Contribution.ACCEPTED
	contribution.save()

	article = contribution.article
	article.content = contribution.change.new_content
	article.save()

	contribution.change.delete()

	return redirect('contributions-list')
```

we first retrieved the contribution and did the necessary permisiions.

Then, the status of the contributio was changed to `Accepted`. notice that we had to save the contribution afterwards. because the changes made to the contribution in the `view` are only reflected to this variable but not saved to the database. the `save()` method is what saves the changes made to the database.
```python
	contribution.status = Contribution.ACCEPTED
	contribution.save()
```

After that we change the articles content to the new content
```python
	article = contribution.article
	article.content = contribution.change.new_content
	article.save()
```

Finally, we delete the change related to this contribution
```python
	contribution.change.delete()
```

###### url
`reading-potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('accept/<int:contribution_id>/', views.accept_changes, name="accept-changes"),
]
```

Now that the accepting functionality is done, you can add a button in the contributions details page to accept the contribution.
`main/templates/contribution_details.html`
```html
...
<a href="{% url 'accept-changes' contribution.id %}"></a>
```