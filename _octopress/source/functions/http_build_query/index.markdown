---
layout: page
title: "JavaScript http_build_query function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/http_build_query:428
- /functions/view/http_build_query
- /functions/view/428
- /functions/http_build_query:428
- /functions/428
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's http_build_query

{% codeblock url/http_build_query.js lang:js https://raw.github.com/kvz/phpjs/master/functions/url/http_build_query.js raw on github %}
function http_build_query (formdata, numeric_prefix, arg_separator) {
  // From: http://phpjs.org/functions
  // +   original by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // +   improved by: Legaev Andrey
  // +   improved by: Michael White (http://getsprink.com)
  // +   improved by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // +   improved by: Brett Zamir (http://brett-zamir.me)
  // +    revised by: stag019
  // +   input by: Dreamer
  // +   bugfixed by: Brett Zamir (http://brett-zamir.me)
  // +   bugfixed by: MIO_KODUKI (http://mio-koduki.blogspot.com/)
  // %        note 1: If the value is null, key and value is skipped in http_build_query of PHP. But, phpjs is not.
  // -    depends on: urlencode
  // *     example 1: http_build_query({foo: 'bar', php: 'hypertext processor', baz: 'boom', cow: 'milk'}, '', '&amp;');
  // *     returns 1: 'foo=bar&amp;php=hypertext+processor&amp;baz=boom&amp;cow=milk'
  // *     example 2: http_build_query({'php': 'hypertext processor', 0: 'foo', 1: 'bar', 2: 'baz', 3: 'boom', 'cow': 'milk'}, 'myvar_');
  // *     returns 2: 'php=hypertext+processor&myvar_0=foo&myvar_1=bar&myvar_2=baz&myvar_3=boom&cow=milk'
  var value, key, tmp = [],
    that = this;

  var _http_build_query_helper = function (key, val, arg_separator) {
    var k, tmp = [];
    if (val === true) {
      val = "1";
    } else if (val === false) {
      val = "0";
    }
    if (val != null) {
      if(typeof val === "object") {
        for (k in val) {
          if (val[k] != null) {
            tmp.push(_http_build_query_helper(key + "[" + k + "]", val[k], arg_separator));
          }
        }
        return tmp.join(arg_separator);
      } else if (typeof val !== "function") {
        return that.urlencode(key) + "=" + that.urlencode(val);
      } else {
        throw new Error('There was an error processing for http_build_query().');
      }
    } else {
      return '';
    }
  };

  if (!arg_separator) {
    arg_separator = "&";
  }
  for (key in formdata) {
    value = formdata[key];
    if (numeric_prefix && !isNaN(key)) {
      key = String(numeric_prefix) + key;
    }
    var query=_http_build_query_helper(key, value, arg_separator);
    if(query !== '') {
      tmp.push(query);
    }
  }

  return tmp.join(arg_separator);
}
{% endcodeblock %}

 - [Raw function on GitHub](https://github.com/kvz/phpjs/blob/master/functions/url/http_build_query.js)

Please note that php.js uses JavaScript objects as substitutes for PHP arrays, they are 
the closest match to this hashtable-like data structure. 

Please also note that php.js offers community built functions and goes by the 
[McDonald's Theory](https://medium.com/what-i-learned-building/9216e1c9da7d). We'll put online 
functions that are far from perfect, in the hopes to spark better contributions. 
Do you have one? Then please just: 

 - [Edit on GitHub](https://github.com/kvz/phpjs/edit/master/functions/url/http_build_query.js)

### Example 1
This code
{% codeblock lang:js example %}
http_build_query({foo: 'bar', php: 'hypertext processor', baz: 'boom', cow: 'milk'}, '', '&amp;');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'foo=bar&amp;php=hypertext+processor&amp;baz=boom&amp;cow=milk'
{% endcodeblock %}

### Example 2
This code
{% codeblock lang:js example %}
http_build_query({'php': 'hypertext processor', 0: 'foo', 1: 'bar', 2: 'baz', 3: 'boom', 'cow': 'milk'}, 'myvar_');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'php=hypertext+processor&myvar_0=foo&myvar_1=bar&myvar_2=baz&myvar_3=boom&cow=milk'
{% endcodeblock %}


### Other PHP functions in the url extension
{% render_partial _includes/custom/url.html %}
