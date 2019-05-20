`authentication/views.py`
```pyhton
from django.contrib.auth import login, authenticate
from .forms import UserLogin, UserRegister
...

def login_view(request):
	form = UserLogin()
	if request.method == 'POST':
		form = UserLogin(request.POST)
		if form.is_valid():
			username = form.cleaned_data['username']
			password = form.cleaned_data['password']

			auth_user = authenticate(username=username, password=password)
			if auth_user is not None:
				login(request, auth_user)
				return redirect('articles-list')

	context = {
        "form":form
    }
	return render(request, 'login.html', context)
```

Since the `UserLogin` is just a `Form` we have to extract the information from it. we can do that after checking that the form is valid. Because after checking the forms validity, we can use the `cleaned_data` dictionary that the form has to get all the information sent through the post request.

```python
username = form.cleaned_data['username']
password = form.cleaned_data['password']
```

After we get the username and password, we check if a user with this username password combination exists using the authenticate method which django provides. This method returns a user if such a combination exists.
```python
auth_user = authenticate(username=username, password=password)
```

Finally, if the above function returned a user, then this user exists and we can log him in.
```python
if auth_user is not None:
	login(request, auth_user)
```