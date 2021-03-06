# Exercise: Display custom variables

**Step 1**: Add the theme file.

This file is a placeholder for preprocess functions for the theme layer. It can set up variables to use in template files, or override the markup of certain elements as well as modifying logic functions.

Create a new file in your folder called **bear_skin.theme**. This file was previously called template.php in Drupal 7. The .theme file serves the exact same purpose, but many of the preprocess functions are different in Drupal 8.


Add one line to start the document
```<?php ```
but **not** a closing PHP ```?>``` tag.

add:

```
use Drupal\Component\Utility\Xss;
use Drupal\Core\Template\Attribute;
```

These will collects, sanitizes, and renders HTML attributes. It optionally passes in an associative array of defined attributes, or add attributes using array syntax. Read more about Drupal 8 attributes [here](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Template%21Attribute.php/class/Attribute/8).

**Step 2**: Define a custom variable

In this Exercise we will define a simple string variable to display in our Twig template.

```
/**
 * Implements preprocess_page() to add a new string variable
 */
function bear_skin_preprocess_page(&$variables) {
  $variables['my_variable'] = "Here is my variable string";
}
```

We wrap this new variable in a preprocess function ```bear_skin_preprocess_page(&$variables, $hook) {}```

A proprocess function intercepts (overrides) and existing Drupal core function. For instance, the original function is [template_preprocess_page](https://api.drupal.org/api/drupal/core!includes!theme.inc/function/template_preprocess_page/8). By replacing "template" with our theme name, we will hook this function and either modify it or add function, variables etc.

**Step 3**: Display your variable
Add this line at the top of your page.html.twig

```<h2>{{ my_variable }}</h2>```

The bear_skin.theme controls variables which are made available to your .html.twig files. In addition to this custom variable here were can pre-process output, and intercept variables to alter them before they are output.