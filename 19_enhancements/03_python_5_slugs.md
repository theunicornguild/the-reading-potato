What is a slug? It's a part of the URL which identifies a particular page on a website in a form readable by users.

Let's try to understand what that means by seeing an example.

Go to `thereadingpotato.com` and choose any article to see its details. you'll notice that the url does not show the id of the article but rather its title. This title that you're seeing in the url is the slug for this specific article.

This is exactly what we want to do. We want to add a slug field for each article. Let's start by modifying the `Article` model.

`main/models.py`
```python
class Article(models.Model):
    title = models.CharField(max_length=250)
    content = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name="articles")
    created_on = models.DateTimeField(auto_now_add=True)
    last_update = models.DateTimeField(auto_now=True)
    slug = models.SlugField(blank=True)
```

The slug should be automatically generated from the title for each article.

```python
from django.template.defaultfilters import slugify

def create_slug(instance, new_slug=None):
    slug = slugify(instance.title)
    if new_slug is not None:
        slug = new_slug
    qs = Article.objects.filter(slug=slug)
    if qs.exists():
        try:
            int(slug[-1])
            if "-" in slug:
                slug_list = slug.split("-")
                new_slug = "%s%s" % (slug[:-len(slug_list[-1])], int(slug_list[-1]) + 1)
            else:
                new_slug = "%s-1" % (slug)
        except:
            new_slug = "%s-1" % (slug)
        return create_slug(instance, new_slug=new_slug)
    return slug
```
This function takes an article object (`instance`) and slugifies its title. So, if the title was `The Art of Potatoes`, the slug would be `the-art-of-potatoes`.
```python
slug = slugify(instance.title)
```
It then checks if there is another article with the same slug, which means there was another article with the same title. If there was, then  it will number this new slug. For example, let's say there are three articles in our website that have the title `The Art of Potatoes`. The first one created will have this slug `the-art-of-potatoes`, the second one this slug `the-art-of-potatoes-1`, and the third one this `the-art-of-potatoes-2`. These numbers were added just to make sure that each article has a unique slug.

We still haven't called this function anywhere, right?
We want a slug to be added to each new article we create. So, we could just call it in the create article view. However, there is even a better way to do it.

We'll be using something called `signals`. A signal is used to trigger an action when a certain event happens.
In our case, the action that we want triggered is the `create_slug` function. 
When do we want it? when an article object is being saved.

Let's see how we can create this signal
`main/models.py`
```python
from django.db.models.signals import pre_save
from django.dispatch import receiver

...
@receiver(pre_save, sender=Article)
def generate_slug(instance, *args, **kwargs):
    if not instance.slug:
        instance.slug=create_slug(instance)
```

What made this function a signal is the `receiver` decorator above it. The `receiver` takes two parameters, the type of the `signal` and the `sender` (a model).

What does the `receiver` do? It waits for an event to happen and then triggers an action.

In this case, the event it waits for is right before Artcle object gets saved.

The action that gets triggered is the `generate_slug` function which takes instance as a parameter which is an article object.

All we did in the function was check if the object has a slug. If it doesn't create one.

This is how everything looks like at the end.
`main/models.py`
```python
from django.db.models.signals import pre_save
from django.dispatch import receiver
from django.template.defaultfilters import slugify
...


class Article(models.Model):
    title = models.CharField(max_length=250)
    content = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name="articles")
    created_on = models.DateTimeField(auto_now_add=True)
    last_update = models.DateTimeField(auto_now=True)
    slug = models.SlugField(blank=True)


def create_slug(instance, new_slug=None):
    slug = slugify(instance.title)
    if new_slug is not None:
        slug = new_slug
    qs = Article.objects.filter(slug=slug)
    if qs.exists():
        try:
            int(slug[-1])
            if "-" in slug:
                slug_list = slug.split("-")
                new_slug = "%s%s" % (slug[:-len(slug_list[-1])], int(slug_list[-1]) + 1)
            else:
                new_slug = "%s-1" % (slug)
        except:
            new_slug = "%s-1" % (slug)
        return create_slug(instance, new_slug=new_slug)
    return slug


@receiver(pre_save, sender=Article)
def generate_slug(instance, *args, **kwargs):
    if not instance.slug:
        instance.slug=create_slug(instance)

...

```

Now that slugs are created, we need to start using them. So, instead of showing the id of an article in the url, we'll show the slug and instead of sending the id to get the article we'll send the slug.

`main/templates/articles_list.html`
```
...
    <a href="{% url 'article-details' article.slug %}">
        <h1>{{article.title}}</h1>
    </a>
...
```

`main/views.py`
```python
def article_details(request, article_slug):
    context = { "article" : Article.objects.get(slug=article_slug)}
    return render(request, 'article_details.html', context)
```

`reading_potato/urls.py`
```python
...
    path('articles/<article_slug>/', views.article_details, name="article-details"),
...
```

Note: any view that is redirecting to the article details page will need to send the slug instead of the id so change those accordingly.

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "added slugs"
$ git push
```
___