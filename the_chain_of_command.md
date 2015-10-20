# The chain of command

There is a chain of command in the types of languages available to the themer. Each language (or scripting language) has its own purpose.

| Language | Purpose |
| -- | -- |
| PHP | Logic and database connection |
| HTML (aka markup) | Creation of the desired markup around the content and scaffolding for the CSS and JS |
| Twig | Templating system |
| CSS | The look of the site |
| JS/JQUERY | User interactions, animations, etc |



---

It is important to use each language for its intended purpose, and to follow the chain of command and attempt to use, for example, javascript to accomplish a CSS task, or to use CSS to cover up something that should be handled in markup or PHP. Violating this command chain for momentary convenience tends to cause problems. Another way to think about it is in terms of each level adding enhancement, as the site should still function as the outer-most layers are stripped away.

![](chain.png)


### Before you do major changes to your theme, check:


* Can you just change a setting in a module or permissions?
* Can it be done with PHP prior to using Javascript?
* Can you accomplish your goal through CSS? 

