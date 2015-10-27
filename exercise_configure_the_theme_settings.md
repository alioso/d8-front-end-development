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