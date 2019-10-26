Declining a Contribution does not require a `template` since there is not a page to be seen after you decline a contribution. So, we will only be needing a `view` and a `url` to that `view`.

What happens when the contribution is declined?
 * the contribution's status is changed to declined
 * the `Change` object conncted to this contribution is deleted

Let's see how it's done

#### view
```python
def decline_changes(request, contribution_id):
	contribution = Contribution.objects.get(id=contribution_id)

	if request.user != contribution.article.author :
		return redirect('articles-list')

	contribution.status = Contribution.DECLINED
	contribution.save()

	contribution.change.delete()

	return redirect('contributions-list')
```

This view is simpler than the `accept-changes` view. All that was done was changing the contributions status, saving it and then finally deleteing the change.

#### url
`reading_potato/urls.py`
```python
...
urlpatterns = [
    ...
    path('decline/<int:contribution_id>/', views.decline_changes, name="decline-changes"),
]
```
 
Just as we did for the accept, we need to add a button in the contribution details for the author to decline this contribution.
`main/templates/contribution_details.html`
```html
...
<a href="{% url 'decline-changes' contribution.id %}">Decline</a>
```

## Trello

> Move card `As a logged in user, I can approve or decline the changes made to my articles` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished accepting and declining contribution functionality"
$ git push
```
