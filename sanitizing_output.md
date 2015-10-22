# Sanitizing output

The two most common security vulnerabilities for Drupal sites are SQL Injection and Cross-site Scripting (XSS). 
SQL Injection attacks can occur when a call to access the database is not protected. Very few calls to the database should occur in themes, so this vulnerability is mainly the concern of module developers. 

Cross-site scripting attacks can occur when user-generated text is output into the markup without protection. A malicious user can then insert javascript into a site with creative results. This is currently the most common type of website security vulnerability. The responsibility to protect against it occurs in Drupal on the markup output layer and as such is the domain of the front-end developer. User-generated content (typically coming in to the theme by way of a form or through a URL), is not sanitized by Drupal on input and it is typically saved in its raw form into the database. The sanitization of the data is expected to happen on display.

Drupal has functions for sanitizing text before display. The religious use of these functions is the key to XSS prevention.

**check_markup**<br>
Because filters can inject JavaScript or execute PHP code, security is vital here. When a user supplies a text format, you should validate it using $format->access() before accepting/using it. This is normally done in the validation stage of the Form API. You should for example never make a preview of content in a disallowed format.

Note: this function should only be used when filtering text for use elsewhere than on a rendered HTML page. If this is part of a HTML page, then a renderable array with a #type 'processed_text' element should be used instead of this, because that will allow cacheability metadata to be set and bubbled up and attachments to be associated (assets, placeholders, etc.). In other words: if you are presenting the filtered text in a HTML page, the only way this will be presented correctly, is by using the 'processed_text' element.

```
$string = "My String";
$filtered_string = check_markup($string);
return $string;
```

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

**t**<br>
Translates a string to the current language or to a given language.

The t() function serves two purposes. First, at run-time it translates user-visible text into the appropriate language. Second, various mechanisms that figure out what text needs to be translated work off t() -- the text inside t() calls is added to the database of strings to be translated. These strings are expected to be in English, so the first argument should always be in English. To enable a fully-translatable site, it is important that all human-readable text that will be displayed on the site or sent to a user is passed through the t() function, or a related function. See the [Localization API](https://www.drupal.org/node/322729) pages for more information, including recommendations on how to break up or not break up strings for translation.

```
$string = "My translatable string";
$filtered_string = t($string);
return $string;
```

check_plain: Removes markup from plain text. Also ensures that special characters like quotes, ampersands and angle brackets will properly display in the browser.
drupal_set_title($node->title);			// Incorrect
drupal_set_title(check_plain($node->title)); 	// Correct
check_markup: Runs rich text through one of the formats configured on the site. Formats contain filters for changing the text. For example, the default Filtered HTML format contains filters that include converting URLs into links and replacing line breaks with <p> and <br /> tags. 
return check_markup($text, ‘filtered_html’);

filter_xss: Removes javascript from URLs, sanitizes dangerous code, ensures that HTML tags and attributes are well-formed, and removes all HTML tags except those specified. Use this when it doesn’t make sense to have a specific format applied.
return filter_xss($text, $allowed_tags = array(‘ul’, ‘ol’, ‘li’));