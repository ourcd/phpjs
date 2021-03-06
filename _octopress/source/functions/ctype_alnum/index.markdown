---
layout: page
title: "JavaScript ctype_alnum function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/ctype_alnum:751
- /functions/view/ctype_alnum
- /functions/view/751
- /functions/ctype_alnum:751
- /functions/751
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's ctype_alnum

{% codeblock ctype/ctype_alnum.js lang:js https://raw.github.com/kvz/phpjs/master/functions/ctype/ctype_alnum.js raw on github %}
function ctype_alnum (text) {
  // From: http://phpjs.org/functions
  // +   original by: Brett Zamir (http://brett-zamir.me)
  // -    depends on: setlocale
  // *     example 1: ctype_alnum('AbC12');
  // *     returns 1: true
  if (typeof text !== 'string') {
    return false;
  }
  // BEGIN REDUNDANT
  this.setlocale('LC_ALL', 0); // ensure setup of localization variables takes place
  // END REDUNDANT
  return text.search(this.php_js.locales[this.php_js.localeCategories.LC_CTYPE].LC_CTYPE.an) !== -1;
}
{% endcodeblock %}

 - [Raw function on GitHub](https://github.com/kvz/phpjs/blob/master/functions/ctype/ctype_alnum.js)

Please note that php.js uses JavaScript objects as substitutes for PHP arrays, they are 
the closest match to this hashtable-like data structure. 

Please also note that php.js offers community built functions and goes by the 
[McDonald's Theory](https://medium.com/what-i-learned-building/9216e1c9da7d). We'll put online 
functions that are far from perfect, in the hopes to spark better contributions. 
Do you have one? Then please just: 

 - [Edit on GitHub](https://github.com/kvz/phpjs/edit/master/functions/ctype/ctype_alnum.js)

### Example 1
This code
{% codeblock lang:js example %}
ctype_alnum('AbC12');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
true
{% endcodeblock %}


### Other PHP functions in the ctype extension
{% render_partial _includes/custom/ctype.html %}
