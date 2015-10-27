# Exercise: Customizing a Field output


### Use Devel and template_preprocess_node to prepare Field data for a node template

**Step 1**: Create an Author field for the Article content type

Under the article content type’s Manage fields, add a new textfield named field_author, titled ‘Author’, to the Article type. Under Display fields, set both the Default and Teaser node display settings to <Hidden> for ‘Author’. By hiding it, we can take control of the display ourselves and not have it appearing it twice.

If you have not done so already, create an article node and fill in all fields.

---

**Step 2**: Create a new variable for the author information

In bear_skin.theme, find or add ```bear_skin_preprocess_node``` so we end up with the following code:

```
function bear_skin_preprocess_node(&$variables) {
  $element = $variables['element'];
  $node = \Drupal::request()->attributes->get('node');
  //kint($variables); 
  if (!empty($node->field_author->value)) {
    $variables['author'] = t("Written by ") . $node->field_author->value;
  }
}

```

In this example we define a $node variable by getting the node attributes, which will allow us to store the author field value in a separate variable "author" if the field contains data. Also notice the ```kint()``` command. Kint will dump all available variables on your page when devel and devel kint modules are enabled. It will allow you to have a quick overview of the variables available for your preprocessing. Just like the twig template suggestions, it is a very helpful debugging tool when writing overrides.

---

**Step 3**: Print out the custom author output on article nodes