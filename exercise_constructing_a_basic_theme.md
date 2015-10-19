# Exercise: Constructing a basic theme

**Step 1**: Go to your /themes/custom folder from youDrupal 8 root folder. 

* ***Create a folder***: bear_skin
* ***Create a text file***: bear_skin.info.yml



No .info file anymore. They have been replaced with Twig and Yaml (.yml) files. The syntax is easy and intuitive, but make sure to check out a few examples as there are conventions to respect. For example, set indentation to spaces, not tabs, respect precise indentation, etc).Read more at http://twig.sensiolabs.org/

In that text file add the following lines:

```
name: My Theme
type: theme
description: ‘My great theme'
package: Custom
core: 8.x
engine: twig

```

