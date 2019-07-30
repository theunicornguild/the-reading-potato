## Trello
> Move card `As a logged in user, I can contribute to any article's content and wait for approval` from the `Backlog` to the `Doing` list.
___


This page allows users to contribute to/edit the content of the article and wait for approval. 

Even though the naming might be different, this is no different than the `edit_article` page. However, in the contribution, the user is only allowed to change the `content` and not the `title`. So, we'll need a new form.

`main/forms.py`
```python
...

class ContributeArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = ['content']
```