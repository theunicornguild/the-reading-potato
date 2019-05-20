Now that our website is expanding, we need a better way to navigate through the pages rather than having to write the url for each page. So, we need to create a `navbar` which will have a link for all the pages that our website provides.

The navbar will be present in all pages. But, it wouldn't make sense to write the code for the navbar in every page. So, instead we'll only write it once in one place and that place is......* thinking time *
![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

yup, that's right. it's the one and only `base.html`.

We'll be just copying a navbar from [bootstrap](https://getbootstrap.com/docs/4.0/components/navbar/). 

`main/templates/base.html`
```html
<html lang="en">
<head>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <a class="nav-item nav-link active" href="#">Home <span class="sr-only">(current)</span></a>
          <a class="nav-item nav-link" href="#">Features</a>
          <a class="nav-item nav-link" href="#">Pricing</a>
          <a class="nav-item nav-link disabled" href="#">Disabled</a>
        </div>
      </div>
    </nav>
    
    {% block content %}

    {% endblock content%}
    
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
</body>
```

We need to make a few changes the `navbar` to make it relevant to our website. We'll start with changing the title in the navbar. Then we'll add links to our pages.

```html
...
 <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="{% url 'articls-list' %}">The Reading Potato</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <a class="nav-link" href="{% url 'login' %}">Login</a>
          <a class="nav-link" href="{% url 'register' %}">Register</a>
          <a class="nav-link" href="{% url 'logoutr' %}">Logout</a>
          <a class="nav-link" href="{% url 'create-article' %}">Create</a>
          <a class="nav-link" href="{% url 'my-articles-list' %}">My Articles</a>
        </div>
        
      </div>
    </nav>
...
```

It's up to you to decide what you want to be shown on the navbar.