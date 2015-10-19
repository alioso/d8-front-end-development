# Review: Anatomy of a theme

For the purposes of this session to see how the Drupal theme system works, we created a theme from scratch. In practice, however, this is not how many developers use the theme layer in Drupal. In the next session, we will see how to use a popular starter theme to quickly set up a custom theme.

Now you have a hands-on understanding of the anatomy of a Drupal theme.

**.info.yml**<br />
This is the only required file of a theme. It defines the theme name, its regions, stylesheets, and other options. Each line defines an option as a key-value pair (key = value). Values not specified will use Drupal’s default.

**Template files**<br />
These files end in *.html.twig <br />
The theme registry stores theme information.
Use a template folders to organize your template files

**CSS files**<br />
Files need to be listed in the .libraries.yml file or included elsewhere with code. Multiple files can be created to keep things organized and modular.
Use folders to organize your CSS files as well.
Many people use sass and a pre-processor nowadays. scss files need to follow the same  structure to keep things well organized.

**JS files**<br />
Files need to be listed in the .libraries.yml file or included elsewhere with code as well.

**images**<br />
Image files that are specific to the theme (background images, svg, sprites etc) should be kept within the theme in an images folder

Images that are not specific to the theme (photo placed inline in a node body, etc) should not be placed in the theme, but should be handled by Drupal and placed/uploaded in its files directory.