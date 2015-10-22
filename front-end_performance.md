# Front-end Performance

The front-end of a site can be a major performance bottleneck. The number of files requested on each page (CSS, Javascript, and images), and the size of these files are the primary performance factors. A high-performance front end begins in the design stage by requiring few and smaller background images (and other assets).


### CSS and JS Aggregation

Due to its modular nature, Drupal sites tend to have many CSS and Javascript files. All of these separate files would be a major performance problem, except for Drupal’s built-in system for aggregating these files into a single CSS and JS file. It also compresses CSS files. This aggregation can be turned on/off on your site at admin/config/development/performance. This is typically done at site launch as the aggregation interferes with theme development.

go to: yoursite/admin/config/development/performance and enable the aggregation for CSS and JS. Look at the result, you'll see all css compressed into one file. Note: if you make changes to your CSS or JS while it is aggregated, you'll need to clear the caches to see the results. 