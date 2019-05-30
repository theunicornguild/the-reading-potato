This is the page where the user can see all the contributions he made to check their status whether accepted, declined, or still pending.

Let's take a look at how the view is made
`main/views.py`
```python
def my_contributions_list(request):
	if request.user.is_anonymous:
		return redirect('login')

	return render(request, "my_contributions_list.html")
```

We started with checking permissions. Then all we did was return the template. 
We didn't retrieve the contributions from the database.
We didn't send anything through the context dictionay.

Then how would we display them in the template?
*thinkung time *
![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

We can get the contributions through the user since the contribution is connected to the user through a `ForeignKey`.