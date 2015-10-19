# Exercise: Constructing a basic theme

**Step 1**: Go to your /themes/custom folder from youDrupal 8 root folder. 

* ***Create a folder***: bear_skin
* ***Create a text file***: bear_skin.info.yml



No .info file anymore. They have been replaced with Twig and Yaml (.yml) files. The syntax is easy and intuitive, but make sure to check out a few examples as there are conventions to respect. For example, set indentation to spaces, not tabs, respect precise indentation, etc).Read more at http://twig.sensiolabs.org/

In that text file add the following lines:

```
name: Bear Skin
type: theme
description: ‘My custom theme'
package: Custom
core: 8.x
engine: twig

```

**Step 2**: On the Appearance page, enable and set Bear Skin to default

Go to your Home page and view your site and view source.
* What can you tell from the look of your site about how Drupal works?
* What was unexpected?
* Do you need to clear the Drupal caches?

**Step 3**: Define your libraries (css and JS) in your bearskin.info.yml file. This is a reference to a bearskin.libraries.yml we will be creating in step 5. Notice the indentation here: “libraries:” will be left aligned while the lines underneath will be indented by 2 spaces.