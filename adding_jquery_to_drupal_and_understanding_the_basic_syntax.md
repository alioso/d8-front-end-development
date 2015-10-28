# Adding jQuery to Drupal and Understanding the basic Syntax

As we've seen in a previous chapter, while jQuery ships with Drupal, it is not being loaded by default, but we called it in our ```bear_skin.libraries.yml``` along with a with a couple helpful libraries.

```
global_scripts:
  version: 1.x
  js:
    js/vendor/modernizr.js: { scope: header }
    js/scripts.js: { scope: header }
  dependencies:
    - core/jquery
    - core/drupal.ajax
    - core/drupal
    - core/drupalSettings
    - core/jquery.once
```

It is also possible to attach your libraries to a single page or subset of pages if you don't want to  load it everywhere as shown [here](https://www.drupal.org/theme-guide/8/assets).

For instance, we can attach JS to a page or a content type with a preprocess function. In this example we add a custom library to the home page only.

```
function bear_skin_preprocess_page(&$variables) {
  if ($variables['is_front']) {
    $variables['#attached']['library'][] = 'bear_skin/custom-library';
  }
}
```

### Syntax


The basic syntax is meant to simplify the writing of Javascript functions. For instance:

```
$(“#content”).hide();
```
```
$(“header a”).addClass(‘main-link’);
```
```
$(“#content div.clickable”).click(function({ 
  $(this).hide(300);              
});
```

Let's remember that while jQuery can leverage a lot of front end issues, modifying the DOM has its drawbacks and should not be a replacement for proper css theming.