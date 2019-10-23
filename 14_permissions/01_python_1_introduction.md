We need to start differentiating between a logged in user, an admin or an anonymous user (not logged in) because some pages require the user to be logged in. Another example is the navbar, if the user is logged in, they should see the logout link. On the other hand, if they're not, they should only see the login and register links.

Basically, a user is either *not* logged in (`anonymous`), logged in (`authenticated`), or an admin (`staff`).

We can check those permissions in both the `templates` and the `views`. 

Let's go over our views and figure out what permissions we want to give each `view`.
 * `articles_list`: Anyone should be able to access it.
 * `article_details`: Anyone should be able to access it.
 * `create_article`: Only `authenticated` users should access it, since the logged in user is added as the author.
 * `my_articles_list`: Only `authenticated` users should access it, since only a logged in user has articles.
 * `register`: Only `anonymous` users can access it. it wouldn't make sense to let a logged in user register.
 * `login_view`: Only `anonymous` users can access it. because why would a logged in user want to login.
 * `logout_view`: Only `authenticated` users should access it. there is no need to explain this one.

What we'll be doing in this chapter is securing our websites and adding permission so that the website is more secure and user friendly at the same time.
