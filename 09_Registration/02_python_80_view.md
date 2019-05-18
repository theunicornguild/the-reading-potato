Since this `view` is for the registration, it has to be written in the `authentication` app.

`authentication/views.py`
```python
from django.shortcuts import render
from django.contrib.auth import login

from forms import UserRegister


def register(request):
	form = UserRegister()
	if request.method == 'POST':
		form = UserRegister(request.POST)
		if form.is_valid():
			user = form.save(commit=False)
			user.set_password(user.password)
			user.save()
			login(request, user)
			return redirect("articles-list")
	context = {
        "form":form,
    }
	return render(request, 'register.html', context)
```

All the steps are almost identical to the `article_create` view. The difference is the password. Django does not allow us to save the password as plain text, we need to hash it first which can be considered as a form of encryption to secure the password. So, we won't save the user to the database yet.
```python
user = form.save(commit=False)
```
Django provides the `User` model with a method called `set_password` which takes the password as plain text, hash it, and then adds it to the `user` object. 
```python
user.set_password(user.password)
```
After that, we save the `user` to the database and then login the user.
```python
user.save()
login(request, user)
```
Django provides us with a function to login the user. All we have to do is give it the `request` and the `user` object.
