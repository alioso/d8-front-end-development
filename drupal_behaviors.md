# Drupal Behaviors

Drupal uses the concept of jQuery behaviors. When a page loads, all the behaviors are run. Behaviors can be asked to load again after the initial page load, for example after an AJAX call adds additional elements to the page. 

We first start with the necessary wrappers in which to put our behaviors. JavaScript should be made compatible with libraries other than jQuery using this:

```
(function ($, Drupal, window, document, undefined) {

 
})(jQuery, Drupal, window, document);
```

This wrapper is an anonymous closure that provides state throughout the page's lifetime and ensures your code does not unintentionally create/override global variables.

It also explicitly imports the global jQuery variable so that your code can use the local $ variable instead of the jQuery global. This is essential because Drupal loads jQuery with noConflict() compatibility so the jQuery library does not setup the normal $ as a global variable.

---

Let's now add a new behavior. Each behavior needs it own name
```
(function ($, Drupal, window, document, undefined) {

  // Use the sample behavior pattern below
  
  Drupal.behaviors.bear_skin = {
   attach: function (context, settings) {
     
     var $element = $('header .element', context);
     $element.hide();
  
    }
  };
 
})(jQuery, Drupal, window, document);
```

In this example, any ```.element``` item will get hidden, even when it is being called through AJAX.

* **bear_skin**: Your unique behavior namespace
* **context**: Behaviors can be fired multiple times during page execution and can be run whenever new DOM elements are inserted into the document.
* **settings**: Is what enables us to pass information from our PHP code to our JavaScript code. This means you can change how your JavaScript behaves based on your module. For example, you may want to simply let JavaScript know what the base path is. In order to do this, you just create a PHP array of settings, as follows.

Additionally, you may not want to to run your code on every request. ```jQuery.once();``` to the rescue! You could add this to your existing code.

```
$element
  .once()
  .hide();
```

or

```
context.once(function() {
  var $element = $('header .element', this);
  $element.hide();
}
```

If you'd rather group some functions under the same ```.once()``` wrapper.

More information about behaviors and debugging jQuery in Drupal is available in this [excellent article](https://www.lullabot.com/articles/understanding-javascript-behaviors-in-drupal).