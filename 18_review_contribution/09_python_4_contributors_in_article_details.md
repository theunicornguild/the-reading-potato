Now that everything related to contributions is done, it's time for us to show the contributors names in the article details page and give them credit for their contributions.

Instead of just retrieving and sending the article's details to the template, we need to retrieve the accepted contributions made to this article as well. And the contributions have the user's information in it.

## Trello
> Move card `As a user, i can see the articles author and all users that contributed in it in the details page` from the `Backlog` to the `Doing` list.
___

`main/views.py`
```python
def article_details(request, article_id):
	article = Article.objects.get(id=article_id)
	contributions = article.contributions.filter(status=Contribution.ACCEPTED)

	context = {
		"article": article,
		"contributions": contributions,
		}
	return render(request, "article_details.html", context)
```

Then in the `article_details.html`, for example if you want display the contributor's first name it'll look like this
```html
{% for contribution in contributions %}
	{{contribution.user.first_name}}
{% endfor %}
```

However, in the case that a user contributed to the same article multiple times, his name will be repeated in the article details page just as many times. So, to fix this problem we can do this to the contributions query.

```python
contributions = article.contributions.filter(status=Contribution.ACCEPTED).distinct('user')
```

This is very straight forward, so I'll let you guess what this does. 

The dancing potato might help.

![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

If even the dancing potato didn't help, I'll just tell you. `distinct` brings all the contributions specified by the query without getting more than one contribution for the same `user`. So, basically the `user` field will be `distinct` in the result of this query.

But, there is still one more problem 

![eye roll](https://media.giphy.com/media/h5YJdPfkSbcRO/giphy.gif)

`distinct` does not work with our local databse, but it works with the deployement database. So, we want to use `distinct` but not locally.

```python
from django.conf import settings
...

def article_details(request, article_id):
	article = Article.objects.get(id=article_id)
	if settings.DEBUG:
		contributions = article.contributions.filter(status=Contribution.ACCEPTED)
	else:
		contributions = article.contributions.filter(status=Contribution.ACCEPTED).distinct('user')

	context = {
		"article": article,
		"contributions": contributions,
		}
	return render(request, "article_details.html", context)
```

This is how we fixed the problem. We first import `settings` file because inside of it there is a variable called `DEBUG`.

`DEBUG` is set to `True` when we're in developement environemnt which means we're working on the project locally on our machines.

`DEBUG` is set to `False` when our project is deployed/live.

So, we fixed the `distict` problem by checking if this value is `True` or `False` and getting the contributions accordingly.

## Trello

> Move card `As a user, i can see the articles author and all users that contributed in it in the details page` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "displaying the contributors in the articles details page"
$ git push
```

