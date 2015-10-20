# Exercise: Intercept and alter

Here is an example exercise where we can intercept the value of an element and override how it looks. A list of available preprocess functions is available at https://api.drupal.org/api/drupal/8/search/preprocess

I'd recommend to bookmark his page as this could become a very needed resource once diving into your theme overrides.

In this example we will add a div around the page title.

```
/**
 * Implements hook_preprocess_page_title
 */
function bear_skin_preprocess_page_title(&$variables) {
  // add a wrapper around the <h1> page title
  if (!empty($variables['title'])) {
    // elements.
    $variables['title_prefix']['wrapper'] = array(
      '#markup' => '<div class="my-custom-wrapper">',
      '#weight' => 100,
    );
    $variables['title_suffix']['wrapper'] = array(
      '#markup' => '</div>',
      '#weight' => -99,
    );
  }
}
```

You can see in this example (and the one following) that the way to override a theme function is to get the right preprcess name (ex: ```function hook_preprocess_page_title(&$variables){}```) and replace "hook" with your theme name in this case. 

*note: if that function were to be in a custom module, the way to override it would be to replace hook with the module name.*


In this second example, we'll add a class to the body tag to show whether the user viewed by an authenticated user or not.

```
/**
 * Implements hook_preprocess_html
 */
function bear_skin_preprocess_html(&$variables, $hook) {
  // Add a class that tells us whether the page is viewed by an authenticated user or not.
  $variables['attributes']['class'][] = $variables['logged_in'] ? 'logged-in' : 'not-logged-in';
}
```

Notice the use of **code commenting** here, both preceding the function and within the function. These are coding standards in Drupal. It helps code readability by explaining which function you are targeting, and what is the goal of the override.

Good commenting practices is especially important for when working with a team. Always keep in mind that you may not be the only maintaining the custom code you wrote.