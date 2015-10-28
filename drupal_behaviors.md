# Drupal Behaviors

Drupal uses the concept of jQuery behaviors. When a page loads, all the behaviors are run. Behaviors can be asked to load again after the initial page load, for example after an AJAX call adds additional elements to the page. 

We first start with the necessary wrappers in which to put our behaviors.

```
(function ($, Drupal, window, document, undefined) {

 
})(jQuery, Drupal, window, document);
```

Each behavior needs it own name
```
(function ($, Drupal, window, document, undefined) {

  'use strict';

  // Use the sample behavior pattern below
  
  Drupal.behaviors.bear_skin = {
   attach: function (context, settings) {
     context = context || document;
     settings = settings || Drupal.settings;
     
     //write your custom code here
  
   }
  };
 
})(jQuery, Drupal, window, document);
```

```

More information about behaviors and debugging jQuery in Drupal is available in this [excellent article](https://www.lullabot.com/articles/understanding-javascript-behaviors-in-drupal).