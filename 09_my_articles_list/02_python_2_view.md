
###### view

`main/views.py`
```python
def my_articles_list(request):
	return render(request, "my_articles_list.html")
```

In this view, we are doing absolutely nothing. The only thing happening is that we're returning the template we're using. So, how can we display the articles belonging to this user, where the author is the user that requested the page. 

I'll give you a hint. the `request` has the user and it's sent to the template. Now take a look at the models and try to figure out how to get those articles.  

![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

Here is the trick, if we can get the user from the request and the model `Article` is connected to the `User` model through a `ForeignKey` then we can get all the articles connected to this user using the `related_name` that we specified in the model.