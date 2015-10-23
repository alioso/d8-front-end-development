# Exercise: Customizing a Field output


### Use Devel and template_preprocess_node to prepare Field data for a node template

**Step 1**: Create an Author field for the Article content type

Under the article content type’s Manage fields, add a new textfield named field_author, titled ‘Author’, to the Article type. Under Display fields, set both the Default and Teaser node display settings to <Hidden> for ‘Author’. By hiding it, we can take control of the display ourselves and not have it appearing it twice.

If you have not done so already, create an article node and fill in all fields.