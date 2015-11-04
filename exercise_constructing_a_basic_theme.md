# Exercise: Constructing a basic theme

**Step 1**: Go to your /themes/custom folder from your Drupal 8 root folder. 

* ***Create a folder***: bear_skin
* ***Create a text file***: bear_skin.info.yml
<br>

Unlike in Drupal 7, themes in Drupal 8 do not have .info files. They have been replaced with Yaml (.yml) files. The syntax is easy and intuitive, but make sure to check out a few examples as there are conventions to respect. For example, set indentation to spaces, not tabs, respect precise indentation, etc). Read more at http://twig.sensiolabs.org/

In that text file add the following lines:

```
name: Bear Skin
type: theme
description: ‘My custom theme'
package: Custom
core: 8.x
engine: twig
screenshot: screenshot.png

```

---

**Step 2**: On the Appearance page, enable and set Bear Skin to default

Go to your Home page and view your site and view source.
* What can you tell from the look of your site about how Drupal works?
* What was unexpected?
* Do you need to clear the Drupal caches?
* 
---

**Step 3**: Define your libraries (css and JS) in your bearskin.info.yml file. This is a reference to a bearskin.libraries.yml we will be creating in step 5. Notice the indentation here: “libraries:” will be left aligned while the lines underneath will be indented by 2 spaces.

```
libraries:
  - bear_skin/global_styling
  - bear_skin/global_scripts
```

This is the place where you can optionaly remove core stylesheets. ex:

```
stylesheets-remove:
  - core/modules/system/css/components/messages.theme.css
```

Notice that a full absolute path from the site root is needed for that purpose. 

---

**Step 4**: Add regions to your bear_skin.info.yml file. These are the same as the core regions. They will work with the core page.html.twig. Notice the indentation should remain consistent with the previous steps.

```
regions:
  header: 'Header'
  navigation: 'Navigation bar'
  highlighted: 'Highlighted'
  help: 'Help'
  content: 'Content'
  sidebar_first: 'First sidebar'
  sidebar_second: 'Second sidebar'
  footer: ‘Footer'
```

---

**Step 5**: Create a bear_skin.libraries.yml in the theme root folder. This is where we will place the code that will point to our css and JS files. Notice that we include here some libraries that Drupal 8 **does not include by default** (jQuery etc).

```
global-scripts:
  version: 1.x
  js:
    js/scripts.js: {}
  dependencies:
    - core/jquery
    - core/drupal.ajax
    - core/drupal
    - core/drupalSettings
    - core/jquery.once

global-styling:
  version: 1.x
  css: 
    theme:
      css/styles.css: {}
      css/print.css: { media: print }
```
The stylesheets have an optional scope option. They can be under a "theme", or "base" etc scope. This will define the weight/order in which they will be loaded. This is important once you get to load external libraries to get a proper order for your styles overrides.

---

**Step 6**: Define your breakpoints

A breakpoint consists of a label and a media query. Media queries are a formal way to encode breakpoints. For instance, a width breakpoint at 40em is written as the media query '(min-width: 40em)'. Breakpoints are really just media queries with some additional metadata, such as name and multiplier information.

Themes and modules can define breakpoints by creating a config file called myThemeOrModule.breakpoints.yml, where myThemeOrModule is the name of your theme or module. In our case, create a bear_skin.breakpoints.yml

Each entry in this file defines one breakpoint, consisting of a machine name, by which the breakpoint entry is uniquely identified e.g. bear_skin.mobile, and it's children defining the breakpoint's properties:

* **label** - A human readable label for the breakpoint.
* **mediaQuery** - Media query text proper ('all and (min-width: 1000px)'.
* **weight** - Positional weight (order) for the breakpoint.<br>
* **multipliers** - Supported pixel resolution multipliers.

*Note*: The order in which breakpoints are arranged through their weight value is extremely important. **Breakpoints with the smallest min-width should have the lowest weight, while breakpoints with the largest min-width should have a larger weight value**. By default, modules will order breakpoints from smallest to largest. However modules can reverse that order if necessary: for example the Responsive Image module takes care of re-ordering breakpoints from largest to smallest based on the weight value.

```
bear_skin.mobile:
  label: mobile
  mediaQuery: ''
  weight: 0
  multipliers:
    - 1x
bear_skin.narrow:
  label: narrow
  mediaQuery: 'all and (min-width: 400px) and (max-width: 1000px)'
  weight: 1
  multipliers:
    - 1x
bear_skin.wide:
  label: wide
  mediaQuery: 'all and (min-width: 1000px)'
  weight: 2
  multipliers:
    - 1x
```

---

**Step 7**: Add CSS to your theme.
Add two folders in your mytheme folder. A css folder and a js folder. 
Add a styles.css and a scripts.js and place them in their newly created respective folders.

Go to your Home page and view your site. At this stage you could override how your site looks entirely with CSS, using the default markup of Drupal.