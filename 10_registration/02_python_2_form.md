For a user to register, he needs to fill a form with his username, password, email and whatever you as the designer of the website see fit. In this website, I decided to ask for their username, first name, last name, email, and password for registration.


So, we first need to create a form. It will be a `ModelForm` and the model will be a `User` since we're using this form to create a `User` object.


However, before we start writing anything, let's go back to when we first created our apps during the setup. Two apps were created, `main` and `authentication`. We said we'd use the `authentication` app for anything authentication related. So, everything registration related will be done in this app.


Do keep in mind that we could've written everything inside the `main` app, there's nothing wrong with that. But, separating things into apps just makes the code cleaner and easier to maintain.


So, Let's go to the `authentication` app for the first time.


![open](https://media.giphy.com/media/eXg8Ij7JgnyDu/giphy.gif)


Create a `forms.py` file in the `authentication` app

`authentication/forms.py`
```pyhton
from django import forms
from django.contrib.auth.models import User


class UserRegister(forms.ModelForm):
    class Meta:
        model = User
        fields = ['username', 'first_name', 'last_name', 'email' ,'password']

        widgets={
            'password': forms.PasswordInput(),
        }
```

The new thing in this form is the `widgets` where it allows us to customize the input fields. In this case we specified that the password field will have the `PasswordInput` as a widget. you can try removing it and adding it to see the difference that it's making.
