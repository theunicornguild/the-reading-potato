
## Trello
> Move card `As a user, I can login using my username and password` from the `Backlog` to the `Doing` list.
___


Logging in is also another form. But, this time it won't be a `ModelForm`. Take a minute and try to think why that is.

![dancing potato](https://media1.tenor.com/images/61497871ab091f01703a3f1a624fb3c4/tenor.gif?itemid=11684043)

The reason this form is just a `Form` because it is not related to any model. We won't be creating or editing an object of a certain model. We just need to create a form where the user can enter the required information.

In the login form, we want the user to enter his username which is a `CharField` and a password which is also a `CharField`

`authentication/forms.py`

```pyhton
...
class UserLogin(forms.Form):
    username = forms.CharField(required=True)
    password = forms.CharField(required=True, widget=forms.PasswordInput())
```