We're finally in the interesting part. This is where we'll start with allowing other users to contribute to the articles. The author will see those contributions and what changes were made to the article and then decide whether they want to accept or decline these changes.

We need to start thinking how we can keep track of what contributions were made by a user and how the author can see those contributions while keeping in mind that the actual article is not chnaged until the author accepts the changes suggested in the contribution.

This means this change is saved in the database. If we're saving something in the database, that means we'll be needing a `model`. 

Let's think this through, what do we need to know about a contribution:
 * the new content
 * the user who contributed
 * the article this contribution is for
 * the status of this contribution (accepted, declined, pending)

`main/models.py`
```python
...
class Contribution(models.Model):
    PENDING = "Pending"
    ACCEPTED = "Accepted"
    DECLINED = "Declined"

    STATUS = (
        (PENDING, PENDING),
        (ACCEPTED, ACCEPTED),
        (DECLINED, DECLINED),
    )

    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name="contributions")
    article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name="contributions")
    new_content = models.TextField()
    status = models.CharField(max_length=10 , choices=STATUS, default=PENDING)
    date = models.DateTimeField(auto_now_add=True)
```

Let's go through each field in this model:
 * `user`: it's a `ForeignKey` to the `User` model. each contribution may only have one user, but each user can have multiple contributions.
 * `article`: it's a `ForeignKey` to the `Article` model. each contribution may be connected to one article, but each article can have multiple contributions.
 * `new_content`: it's just a text field containing the new content that was contributed.
 * `status`: it's a `CharField` but with choices which means we can only save in it the choices in the `STATUS` array. So, a contribution is either Pending, Accepted, or Declined.
 * `date`: The will automatically be added when the contribution object is created.

What happens to the contribution when it's accepted or declined?

If a contribution is accepted, then the new content should replace the content of the article.
If a contribution is declined, nothing happens other than that the status changed.

In both cases, we'll have different versions of the `content` of the same article saved in each contrbution. However, we can't delete the contribution object because a user would like to know where they contributed and whether their contribution was accepted or not. but saving the contents of each contribution is unnecessary unless we wanted to have all the previous versions.

What I wanted to do was be able to delete the `content` of all the contributions after it's accepted or declined. To do that, I seperated it into a new model.

`main/models.py`
```python
class Contribution(models.Model):
    PENDING = "Pending"
    ACCEPTED = "Accepted"
    DECLINED = "Declined"

    STATUS = (
        (PENDING, PENDING),
        (ACCEPTED, ACCEPTED),
        (DECLINED, DECLINED),
    )

    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name="contributions")
    article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name="contributions")
    status = models.CharField(max_length=10 , choices=STATUS, default=PENDING)
    date = models.DateTimeField(auto_now_add=True)

    

class Change(models.Model):
    new_content = models.TextField()
    contribution = models.OneToOneField(Contribution, on_delete=models.CASCADE)

    def __str__(self):
        return str(self.contribution.article)
```

The `new_content` was removed from the `Contribution` model and added to the new model `Change`. the `Change` model is connected to the `Contribution` model through a one to one relationship. So, each contribution has one change and vice versa. However, in this case we can delete the new content after the status of the contribution changes.

**Important**: Whenever you add/delete a model or modify a model in any way for example renaming or adding new fields, you need to `makemigrations` and `migrate`. By doing this you inform your database of these new changes so that it modifies its tables accordingly.

Make sure you virtual environment is activated and that you're in your project directory and start migrating
```
(env) $ python manage.py makemigrations
(env) $ python manage.py migrate
```

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "added the Contribution and Change models"
$ git push
```
___