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
  if ($variables['node']->getType() === 'article') {
    //kint($variables); 
    if (!empty($node->field_author->value)) {
      $variables['author'] = t("Written by ") . $node->field_author->value;
    }
  }
}

```

In this example we define a $node variable by getting the node attributes, which will allow us to store the author field value in a separate variable "author" if the field contains data. Also notice the ```kint()``` command. Kint will dump all available variables on your page when devel and devel kint modules are enabled. It will allow you to have a quick overview of the variables available for your preprocessing. Just like the twig template suggestions, it is a very helpful debugging tool when writing overrides.

---

**Step 3**: Print out the custom author output on article nodes

Create a ```node--article.html.twig``` and paste the following code, initially take and modified from ```node.html.twig```.

```

{%
  set classes = [
    'node',
    'node--type-' ~ node.bundle|clean_class,
    node.isPromoted() ? 'node--promoted',
    node.isSticky() ? 'node--sticky',
    not node.isPublished() ? 'node--unpublished',
    view_mode ? 'node--view-mode-' ~ view_mode|clean_class,
    'clearfix',
  ]
%}
{{ attach_library('classy/node') }}
<article{{ attributes.addClass(classes) }}>
  <header>
    {{ title_prefix }}
    {% if not page %}
      <h2{{ title_attributes.addClass('node__title') }}>
        <a href="{{ url }}" rel="bookmark">{{ label }}</a>
      </h2>
    {% endif %}
    {{ title_suffix }}
    {% if display_submitted %}
      <div class="node__meta">
        {{ author_picture }}
        <span{{ author_attributes }}>
          {% trans %}Submitted by {{ author_name }} on {{ date }}{% endtrans %}
        </span>
        {{ metadata }}
      </div>
    {% endif %}
  </header>
  <div{{ content_attributes.addClass('node__content', 'clearfix') }}>
    <div style="padding: 30px; margin: 30px 0; border: 1px solid #ccc; color#fff;">{{ author }}</div>
    {{ content }}
  </div>
</article>

```

The line we added here is ```<div style="padding: 30px; margin: 30px 0; border: 1px solid #ccc; color#fff;">{{ author }}</div>``` which passes the variable we defined in ```bear_skin.theme```. I added some inline css to make the field more prevalent, but as always it is better to add a class and theme it within your stylesheet. 

---

*Note:* **In many cases, the best practice to customize a Field display is to create a custom Field formatter in a custom module. With a custom formatter you can easily reuse the format from within Fields, Views, and Panels interfaces. The creation of custom Field formatters can be done in a custom module.**

