# Exercise: Change the default administrative theme

Best practice during theme development is to ensure you have a stable administration theme should anything go awry while working on your site’s design. 

* **Step 1**: In the Toolbar, click on Appearance. Scroll down to the section labeled “Administration theme” and set the administration theme.  Notice you can choose whether to use this theme for content creation as well. Notice how now the theme changes when you go to a path beginning with /admin.

![](admin-theme.png)

---

**Contributed Admin Themes**:
Drupal core comes with an admin theme called Seven. At this time, very few Drupal 8 admin themes are production ready. 

---

* **Step 2**: Look at the blocks administration page (admin/structure/block).

![](blocks.png)

Each theme can have its own block configuration (you can switch from one theme to another within this page).

In this screenshot, we can see the blocks enabled for bear_skin, placed in the regions we defined in ```bear_skin.info.yml```. To add a block you don't see yet, you must choose a region a click the "Place block" button. From there you'll access an overlay that allows you to pick from all blocks available (core blocks, views blocks etc). 

Additionally, each block you have visibility settings (for instance, if you only want the block to show on the home page, or for a specific content type). 


