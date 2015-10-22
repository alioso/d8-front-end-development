# Exercise: Overriding Views Templates

Views templates are very similar to core templates, and have their own naming conventions based on their target. Templates can be specific to a given view, a particular field, an entire display style, or any combination of those. Views now ship with Drupal Core, so let's dive right in.

**Step 1**: Place the Recent Comments block in a region.

Views provides several default views as examples. One example is Recent Comments (comments_recent), which creates both a block displaying the most recent comments with a link to the node. This view is enabled by default. You need to have the comment module enabled and to have some comments on the site.


**Step 2**: Explore the possible templates

To help pick from the various possibilities of a views template name, Views provides a section titled “Theme: Information” within “Advanced”.  Notice that there are different templates for display, style, row style and fields.