We did alot in this chapter so it might be a good idea to go through it quickly.


First to make the contribution actually work, we added two new models `Contribution` and `Change` to save peoples contrubutions that are awaiting acceptance or rejection.


Next, We had to create a form for the user to be able to change the article's content. Then, when this form is submitted with the new article content, a `Contribution` and a `Change` object are created to save this contribution for review.


Test out the page that you just did and make sure everything works error free. If there are any problems fix them then move on to the next chapter.

## Trello

> Move card `As a logged in user, I can contribute to any article's content and wait for approval` to the `Review` list if someone will needs to review it, otherwise move it to `Done`.
___

### Git

Create a new checkpoint

```shell
$ git add .
$ git commit -m "finished contributing functionality"
$ git push
```
___
