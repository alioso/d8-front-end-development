# Exercise: Create a bear_skin Subtheme

Sub-themes are just like any other theme, with one difference: They inherit the parent theme's resources. There are no limits on the chaining capabilities connecting sub-themes to their parents. A sub-theme can be a child of another sub-theme, and it can be branched and organized however you see fit. This is what gives sub-themes great potential.

Since we have created our own **bear_skin** starter theme, we are going to use it as a base theme for our new **bear_coat** sub theme.

**Step 1**: Create a theme_coat folder and place it either: 

* within you starter theme 

mysite > core > themes > custom > bear_skin

* or on the same level at

mysite > core > themes > custom

In our case we will place it within our starter theme, as this facilitates our git workflow.

All you need to get it registered is to include the base theme line in your subtheme bear_coat.info.yml

```
name: Bear Coat
type: theme
description: 'Bear Skin Sub Theme with better styling'
package: Custom
core: 8.x
engine: twig
base theme: bear_skin
screenshot: screenshot.png
```