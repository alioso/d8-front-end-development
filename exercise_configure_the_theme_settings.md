# Exercise: Configure the theme settings

Drupal comes with some theme settings that can be configured in the administrative UI. This is where some of the site identity assets are defined, as well as a couple of other miscellaneous settings. A Global Settings page located at admin/appearance/settings will define your defaults. but each enabled theme can override these and have its own custom settings.

This functions exactly like Drupal 7. Add a ```theme-settings.php``` in your theme root folder and follow these steps.

**Step 1:**<br>
Open with ```<?php``` tag and write comments to explain what you do or expose some usable variables.
**Don't close the your PHP tag!**

---

**Step 2:**<br>
Define your function.

```
function bear_skin_form_system_theme_settings_alter(&$form, &$form_state, $form_id = NULL) {

}
```

This function overrides the form at ```/admin/appearance/settings/bear_skin```. Next we will populate that function with custom options.

---

**Step 3:**<br>
Let's first create a fieldset that will contain our custom options so they are grouped together. 

```
$form['bear_options'] = array(
  '#type' => 'fieldset',
  '#title' => t('Bear Skin Theme Additional Options'),
);
```

Next we will place our available options within that fieldset.

---

**Step 4:**<br>
In this step we are going to add two options. One to choose between two layouts (radio button), the other to set a sticky footer or not.

```
// create an option to choose between fixed and fluid layouts
  $form['bear_options']['main_layout'] = array(
    '#type' => 'radios',
    '#title' => t('General Layout'),
    '#description' => t('This option will allow you to pick between a full width (fluid) layout (for background, banners etc, content still has max width) and fixed layout.'),
    '#options' => array(
      'fluid' => t('Fluid'),
      'fixed' => t('Fixed'),
    ),
    '#default_value' => theme_get_setting('main_layout'),
  );

  // create an option for sticky footers
  $form['bear_options']['sticky_footer'] = array(
    '#type' => 'checkbox',
    '#title' => t('Add sticky footer.'),
    '#description' => t('More info about sticky footer <a href="http://www.cssstickyfooter.com/" target="_blank">here</a><br />
      You can change these settings in the the sticky-footer.css file located in the css folder.'),
    '#default_value' => theme_get_setting('sticky_footer'),
  );
```

The code here is pretty straight forward. The key is setting the ```#default_value``` as ```theme_get_setting()``` to pass make these options available for our preprocess functions.

Save your files and clear your caches. Now you should be able to see these new options at ```/admin/appearance/settings/bear_skin```. However, while these options will get stored on save, they do nothing on their own, simply because we have not added any related function yet.

Your final theme-settings.php should look something like that:

```
<?php
/**
 * Implements hook_form_system_theme_settings_alter().
 *
 * @param $form
 *   Nested array of form elements that comprise the form.
 * @param $form_state
 *   A keyed array containing the current state of the form.
 */
function bear_skin_form_system_theme_settings_alter(&$form, &$form_state, $form_id = NULL) {
  $form['bear_options'] = array(
    '#type' => 'fieldset',
    '#title' => t('Bear Theme Additional Options'),
  );

  // create an option to choose between fixed and fluid layouts
  $form['bear_options']['main_layout'] = array(
    '#type' => 'radios',
    '#title' => t('General Layout'),
    '#description' => t('This option will allow you to pick between a full width (fluid) layout (for background, banners etc, content still has max width) and fixed layout.'),
    '#options' => array(
      'fluid' => t('Fluid'),
      'fixed' => t('Fixed'),
    ),
    '#default_value' => theme_get_setting('main_layout'),
  );

  // create an option for sticky footers
  $form['bear_options']['sticky_footer'] = array(
    '#type' => 'checkbox',
    '#title' => t('Add sticky footer.'),
    '#description' => t('More info about sticky footer <a href="http://www.cssstickyfooter.com/" target="_blank">here</a><br />
      You can change these settings in the the sticky-footer.css file located in the css folder.'),
    '#default_value' => theme_get_setting('sticky_footer'),
  );
}
```

---

**Step 5:**<br>
In ```bear_skin.theme``` let's modify or add (if you have not already have one - duplicate functions will break your site.<br>
```
function bear_skin_preprocess_html(&$variables, $hook) {
}
```

In this function we are going to use our ```theme_get_setting``` to set up classes to the body depending on the options we set in the theme settings.

```
// add class depending on Theme layout settings
$variables['fixed_layout'] = (theme_get_setting('main_layout') == 'fixed');
$variables['fluid_layout'] = (theme_get_setting('main_layout') == 'fluid');
if (theme_get_setting('main_layout') == 'fixed') {
  $variables['attributes']['class'][] = 'fixed-bear';
} else if (theme_get_setting('main_layout') == 'fluid') {
  $variables['attributes']['class'][] = 'fluid-bear';
}

```
**and**

```
// if the sticky footer option is selected, set a class
if (theme_get_setting('sticky_footer')) {
  $variables['attributes']['class'][] = 'with-sticky-footer'; // working
}
```

*Notice that still use comments to explain what we are doing.*

For both functions we add a ```$variables['attributes']['class'][] = "something"``` depending on the theme setting value. We can add as many options as possible to leverage theming options through the UI and help a user configure options easily. 