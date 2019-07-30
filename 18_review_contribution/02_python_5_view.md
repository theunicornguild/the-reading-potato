`main/views.py`
```python
...
import difflib

def contribution_details(request, contribution_id):
	contribution = Contribution.objects.get(id=contribution_id)
	if request.user != contribution.article.author:
		return redirect('articles-list')

	d = difflib.Differ()
	comparison = list(d.compare(contribution.article.content.splitlines(True), contribution.change.new_content.splitlines(True)))


	context = {
		"contribution" : contribution,
		"comparison" : comparison,
	}
	
	return render(request, 'contribution_details.html', context)
```

There is nothing special in this `view` , we just retrieved the contribution, added the permissions, and then compared the two strings and sent the result through the context dictionary. 

The actual work will be in the template, because we just sent a list of strings through the `context` dictionary. Now, it's the template's job to show them in a presentable way for the user to be able to know the differences between the current and new content.