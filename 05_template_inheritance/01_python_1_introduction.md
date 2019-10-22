`template inheritance` is a way for us to decrease redundant code. we'll be doing that by creating a template with the things that are in common with all the pages and remove these redundancies from all the templates and instead make them `inherit` the code from the base template.


This isn't considered a functionality or a feature. It's just a way to divide the code and make it cleaner and therefore easier to maintain and debug.


If you open the live demo, you'll notice that the same navbar is in all the pages. The html for the navbar was added in one template and all the other templates inherited from it. So, we only had to write the navbar html once and use it everywhere using `template inheritance`.
