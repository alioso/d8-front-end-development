# Sanitizing output

The two most common security vulnerabilities for Drupal sites are SQL Injection and Cross-site Scripting (XSS). 
SQL Injection attacks can occur when a call to access the database is not protected. Very few calls to the database should occur in themes, so this vulnerability is mainly the concern of module developers. 

Cross-site scripting attacks can occur when user-generated text is output into the markup without protection. A malicious user can then insert javascript into a site with creative results. This is currently the most common type of website security vulnerability. The responsibility to protect against it occurs in Drupal on the markup output layer and as such is the domain of the front-end developer. User-generated content (typically coming in to the theme by way of a form or through a URL), is not sanitized by Drupal on input and it is typically saved in its raw form into the database. The sanitization of the data is expected to happen on display.

Drupal has functions for sanitizing text before display. The religious use of these functions is the key to XSS prevention.

**Html::escape**<br>
Escapes text by converting special characters to HTML entities.

This method escapes HTML for sanitization purposes by replacing the following special characters with their HTML entity equivalents:

* ```&``` (ampersand) becomes ```&amp;```
* ```"``` (double quote) becomes ```&quot;```
* ```'``` (single quote) becomes ```&#039;```
* ```<``` (less than) becomes ```&lt;```
* ```>``` (greater than) becomes ```&gt;```


Special characters that have already been escaped will be double-escaped (for example, ```&lt;``` becomes ```&amp;lt;```), and invalid UTF-8 encoding will be converted to the Unicode replacement character ("�").

```
$string = "My String with this & Character";
$safe_string = Html::escape($string);
return $safe_string;
```
Don't forget to add your include at the top of your .theme file, right after the opening ```<?php``` tag:

```
use Drupal\Component\Utility\Html;
```

check_plain: Removes markup from plain text. Also ensures that special characters like quotes, ampersands and angle brackets will properly display in the browser.
drupal_set_title($node->title);			// Incorrect
drupal_set_title(check_plain($node->title)); 	// Correct
check_markup: Runs rich text through one of the formats configured on the site. Formats contain filters for changing the text. For example, the default Filtered HTML format contains filters that include converting URLs into links and replacing line breaks with <p> and <br /> tags. 
return check_markup($text, ‘filtered_html’);

filter_xss: Removes javascript from URLs, sanitizes dangerous code, ensures that HTML tags and attributes are well-formed, and removes all HTML tags except those specified. Use this when it doesn’t make sense to have a specific format applied.
return filter_xss($text, $allowed_tags = array(‘ul’, ‘ol’, ‘li’));