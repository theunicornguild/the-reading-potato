This is the page where all our reading potatoes will browse through the available articles to read from.

But the question is where are we getting those articles from?
We need to store them somewhere to be able to retrieve them whenever a user requests this page. this storage is the `database` where we can save all our data from users that register in our website to these articles. `Django` provides us with a local database. All we have to do is set the structure of the tables/objects that we're saving there.

what's great about `django` is that it provides a simple way to structure our database and access it through the `models`. 

A `model` essentially creates the structure or maps to a table in your database. It sets the essential fields and the behavior of the information that you want to store.

So, basically all we have to do is set the structure of our `Article` model. If you remember the structure of an `app` folder, you can probably guess where we need to write our `models`. 

Find the `main/models.py` file, and add the following:
```python
from django.db import models
from django.contrib.auth.models import User


class Article(models.Model):
    title = models.CharField(max_length=250)
    content = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name="articles")
    created_on = models.DateTimeField(auto_now_add=True)
    last_update = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

So now, our model has these fields:
  * `title` : a character field which is basically a string
  * `content`: a string
  * `created_on`: stores both date and time and the value is added automatically whenever a page object is created.
  * `last_update`: stores both date and time and the value is added automatically whenever a page object is updated.
  * `author`:  stores the `User` that created this `Page` object, where the `User` is a predefined model created by `Django`. and the `ForeignKey` relationship is a one-to-many which means each `Article` can only be connected to one `User` as the author while the `User` can be connected(be the author) to many `Article` objects.

Every model that we create or any changes we make to a model aren't applied to the `database` immediately. For these changes to take place in our database we need to do what's called `migrations`. `migrations` are basically `django`'s way of converting what we write in the `models` to the actual database, by creating/deleting a table or adding or even renaming a field, and so on. 

To migrate, you need to do two steps:
 * `makemigrations` : converting what is written in the `models.py` to files/migrations which specify the changes made to the model.
 * `migrate`: applies the created `migrations` to the database.

In the terminal:
```shell
(env) $ python manage.py makemigrations
(env) $ python manage.py migrate
```