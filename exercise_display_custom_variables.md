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
function puppet_preprocess_page(&$variables) {
	$variables['my_message'] = 'Oh! I see my variable now.';
}xw
Step 3: Display in page.tpl.php
Add this line at the bottom of  your page.tpl.php
<h1>My message: <?php print $my_message; ?></h1>
The template.php controls variables which are made available to your tpl.php files. In addition to this custom variable here were can pre-process output, and intercept variables to alter them before they are output. 
