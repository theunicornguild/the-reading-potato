Let's go through everything we've done in this chapter.

 * We created the `Article` model so we can save `Article` objects in the database.
 * Then we created a view that retrieves all the articles from the database and returns a `template`.
 * We displayed the information(the articles) sent from the context dictionary in the template.
 * Finally we connected a url/path to the view.


If everything went right, you should now see a list of articles when you open this url `http://127.0.0.1:8000/articles/`. If it's still not working, try to debug it and find where the problem is. It might be just that you didn't add any articles in the admin page. Make sure you don't have any misspellings such as calling `article_list` in the `urls.py` instead of `articles_list`. Go through everything we've done in this chapter and try to find out what the problem is and fix it before continuing into the next chapter. 


If it's working, you can move your trello card and push your code.


## Trello
> Move card `As a user, I can see the list of articles` from the `Doing` to the `Review` list if someone needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished articles list functionality"
$ git push
```
___
