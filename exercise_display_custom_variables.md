# Exercise: Display custom variables

**Step 1**: Add the theme file.
Create a new file in your folder called **bear_skin.theme**. This file was previously called template.php in Drupal 7. The .theme file serves the exact same purpose, but many of the preprocess functions are different in Drupal 8.


Add one line to start the document
```<?php ```
but do not close the with ```?>```

add:

```
use Drupal\Component\Utility\Xss;
use Drupal\Core\Template\Attribute;
```

**Step 2**: Define a custom variable

```
function bear_skin_preprocess_page(&$variables, $hook) {
  $variables['my_variable'] = "Here is my variable string";
}
```

**Step 3**: Display your variable
Add this line at the top of your page.html.twig

```<h2>{{ my_variable }}</h2>```

The bear_skin.theme controls variables which are made available to your .html.twig files. In addition to this custom variable here were can pre-process output, and intercept variables to alter them before they are output. 

Step 3: Display your varialble in page.tpl.php
Add this line at the bottom of  your page.tpl.php
<h1>My message: <?php print $my_message; ?></h1>
The template.php controls variables which are made available to your tpl.php files. In addition to this custom variable here were can pre-process output, and intercept variables to alter them before they are output.