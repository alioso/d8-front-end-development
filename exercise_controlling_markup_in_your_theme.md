# Exercise: Controlling markup in your theme

**Step 1**: Create a templates folder and add a page.html.twig file within.
The easiest way to start is to copy the core page.html.twig into your theme folder.

The core file can be found at:

bear_skin > core > modules > system > templates

To get started you can copy the code from this file and start customizing it for your own needs. Be warned! There are many necessary variables to add to page.html.twig. Refer to: https://api.drupal.org/api/drupal/core%21modules%21system%21templates%21page.html.twig/8

**Step 2**: Identify common variables in page.html.twig

*General utility variables:*

* **base_path**: The base URL path of the Drupal installation. Will usually be "/" unless you have installed Drupal in a sub-directory.
* **is_front**: A flag indicating if the current page is the front page.
* **logged_in**: A flag indicating if the user is registered and signed in.
* **is_admin**: A flag indicating if the user has permission to access administration pages.


*Site identity:*

* **front_page**: The URL of the front page. Use this instead of base_path when linking to the front page. 
This includes the language domain or prefix.
* **logo**: The url of the logo image, as defined in theme settings.
* **site_name**: The name of the site. This is empty when displaying the site name has been disabled in the theme
 settings.
* **site_slogan**: The slogan of the site. This is empty when displaying the site slogan has been disabled in theme
settings.

This is also how the regions are printed onto the page. Locate the ```{{ page.sidebar_first }}``` region in the page.html.twig

page.html.twig will be your first template file. You can see how you can alter the markup directly around the variables. Make sure to include that file within the templates folder and clear your caches for the template to become active. 