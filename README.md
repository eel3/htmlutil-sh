htmlutil-sh
===========

Primitive utilities for CGI/sh.

License
-------

zlib License.

Target environments
-------------------

Cygwin, Linux, Mac OS X.

All scripts are shell script (sh),
and so probably work fine on other Unix-like environment.

Set up
------

Put all scripts in a directory registered in PATH.

Usage
-----

Please check help message `<script-file-name> -h`, or read scripts.

Example
-------

```sh
## HTML escape
echo '<script>alert("XSS")</script>' | escape-html
#=> &lt;script&gt;alert(&quot;XSS&quot;)&lt;/script&gt;

escho-html '<script>alert("XSS")</script>'
#=> &lt;script&gt;alert(&quot;XSS&quot;)&lt;/script&gt;

user='<script>alert("XSS")</script>'
echo "<p>hello, $user.</p>"
#=> <p>hello, <script>alert("XSS")</script>.</p>

echo "<p>hello, `escho-html "$user"`.</p>"
#=> <p>hello, &lt;script&gt;alert(&quot;XSS&quot;)&lt;/script&gt;.</p>

## JavaScript string escape
echo -n '"; alert("XSS");"' | escape-jsstr
#=> \u0022\u003B\u0020\u0061\u006C\u0065\u0072\u0074\u0028\u0022\u0058\u0053\u0053\u0022\u0029\u003B\u0022$

escho-jsstr '"; alert("XSS");"'
#=> \u0022\u003B\u0020\u0061\u006C\u0065\u0072\u0074\u0028\u0022\u0058\u0053\u0053\u0022\u0029\u003B\u0022$

user='"; alert("XSS");"'
echo "<script>var user_name = \"$user\";</script>"
#=> <script>var user_name = ""; alert("XSS");"";</script>

echo "<script>var user_name = \"`escho-jsstr "$user"`\";</script>"
#=> <script>var user_name = "\u0022\u003B\u0020\u0061\u006C\u0065\u0072\u0074\u0028\u0022\u0058\u0053\u0053\u0022\u0029\u003B\u0022";</script>

## XML escape
echo '<book isbn="9780139376818" title="The Unix Programming Environment" />' | escape-xml
#=> &lt;book isbn=&quot;9780139376818&quot; title=&quot;The Unix Programming Environment&quot; /&gt;

## RFC-2616 HTTP-date style date and time
LANG=C TZ=JST-9 date
#=> Thu Sep 25 22:30:10 JST 2014

# current date and time
http-date
#=> Thu, 25 Sep 2014 13:30:10 GMT

# mtime (modify time) of file
http-mtime foo.txt
#=> Thu, 23 Sep 2014 02:37:55 GMT
```
