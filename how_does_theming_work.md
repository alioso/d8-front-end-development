# How does theming work?

When a page is requested from a Drupal site, the PHP code in Drupal’s core files gets the relevant data from the database as needed while it runs through all of its logic and prepares data for display as HTML. As it does this it also interacts with contributed modules which similarly can get and prepare data. Drupal’s core and contributed modules render sections of generated HTML/TWIG and CSS/JS files, doing a good bit of front-end work on their own. The theme mainly overrides and enhances the way the data is prepared for display and can add CSS and JS files of its own. These overrides happen on the CSS level as well as on the HTML/TWIG templating level. The job of the Drupal themer is to work with CSS and JS files and to customize the HTML markup through PHP templates overrides in order to match a design.  

On the file level, each theme is a directory named uniquely with a machine name (underscores and letters only).  This name should not match the name of any module used on the site. Custom and contributed themes belong in your site’s /sites/all/themes directory (you’ll need to make that directory), and core themes, which should not be altered, are in the /themes directory.

![](folder-org.png)



---

Exercise: Add a contributed theme
Step 1: Choose a theme from drupal.org/project/themes and download it. Make sure the theme’s version compatibility matches your version of Drupal core (8.x).
Step 2: Unpack the download and move the directory to /themes/contrib in your codebase.
Step 3: Enable the theme and set is as the default on the Appearance page. Then configure the theme. Some themes will come with more settings you can configure than others.