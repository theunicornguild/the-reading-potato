Let's go over what we've done in this chapter:
 
 * we've created a form with two fields, username and password.
 * we've created a view that returns an empty form or retruievd the sent information and authenticates the user.
 * we've displayed the form in a template.

You must've noticed by now that creating any page goes through the exact process. `url` calls a `view`, and the `view` returns a `template` for the user to see. The difference between each page is the logic happening in the view and the information displayed in the template. 


Now just test your code and move to the next chapter.


## Trello
> Move card `As a user, I can login using my username and password` from the `Doing` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished login functionality"
$ git push
```
___