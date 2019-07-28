It's about time that our website starts looking more representable. We'll be using bootsrap to help us with styling.
Setting up bootstrap to use is very easy. They provide CDNs for their CSS and JS files.

What is a CDN?
CDN stands for Content Delivery Network. In simple terms, think of it as an online link to the CSS or JS files.
Kind of like a dropbox link to an image. But instead it's a link to a CSS/JS file.

To read more about CDNs, click [here](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/).
You should be able to find Bootstrap's CDNs [here](http://getbootstrap.com/docs/4.0/getting-started/introduction/#quick-start).

There's 1 for CSS and 3 for JS. You'll want to copy and paste those into your `base.html` file.
Let's see how that's done.

`main/templates/base.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
</head>
<body>
    {% block content %}

    {% endblock content%}
    
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
</body>
```

After setting up bootstrap, you can now start styling your templates. However, keep in mind that bootstrap is set up in the `base.html` only. Therefore, only templates that are inheriting the `base.html` template have bootstrap.