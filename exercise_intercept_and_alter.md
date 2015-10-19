# Exercise: Intercept and alter

Here is an example exercise where we can intercept the value of an element and override how it looks. A list of available preprocess functions is available at https://api.drupal.org/api/drupal/8/search/preprocess

I'd recommend to bookmark his page as this could become a very needed resource once diving into your theme overrides.

In this example we will add a div around the page title.

```
function bear_skin_preprocess_page_title(&$variables) {
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

You can see in this example (and the one following) that the way to override a theme function is to get the right preprcess name (ex: ```function hook_preprocess_page_title(&$variables){}```) and replace "hook" with your theme name in this case. *note: if that function were to be in a custom module, the way to override it would be to replace hook with the module name.*


