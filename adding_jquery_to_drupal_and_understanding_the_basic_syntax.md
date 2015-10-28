# Adding jQuery to Drupal and Understanding the basic Syntax

As we've seen in a previous chapter, while jQuery ships with Drupal, it is not being loaded by default, but we called it in our ```bear_skin.libraries.yml``` along a with a couple helpful libraries.

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

