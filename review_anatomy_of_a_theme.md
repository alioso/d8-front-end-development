# Review: Anatomy of a theme

For the purposes of this session to see how the Drupal theme system works, we created a theme from scratch. In practice, however, this is not how many developers use the theme layer in Drupal. In the next session, we will see how to use a popular starter theme to quickly set up a custom theme.

Now you have a hands-on understanding of the anatomy of a Drupal theme.

**.info.yml**<br />
This is the only required file of a theme. It defines the theme name, its regions, stylesheets, and other options. Each line defines an option as a key-value pair (key = value). Values not specified will use Drupal’s default.

Additional processing and logic for a theme takes place here. It can override output of other modules via theme function overrides (see http://drupal.org/node/173880#function-override). It can define and edit variables to be used by template files with preprocess functions (see http://drupal.org/node/223430).
template files
These files end in *.tpl.php. Default templates include page.tpl.php, node.tpl.php, block.tpl.php and others (see http://drupal.org/node/1089656 for more). 
The theme registry stores theme information, it must be cleared when new files are added (see http://drupal.org/node/173880#theme-registry)
Use folders to organize your template files
css files
Files need to be listed in the .info file or included elsewhere with code
Multiple files can be created to keep things organized
Use folders to organize your CSS files 
js files
These must be included from code, typically from inside template.php
images
Image files that are specific to the theme (background images, buttons, etc) should be kept within the theme in an images folder
Images are mainly called by CSS files as backgrounds
Images that are not specific to the theme (photo placed inline in a node body, etc) should not be placed in the theme, but should be handled by Drupal and placed in its files directory