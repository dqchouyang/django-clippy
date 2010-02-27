django-clippy - Writing to the Clipboard from within Webpages
=============================================================

django-clippy provides a template tag for the [Django Web Framework][1] 
to allow copying the Clipboard.

    {% load clippy %}
    <p><input id="clipfield" value="Data in Field"> {% clippy "clipfield" %}

Here is what Clippy looks like on GitHub:

![Clippy in action](http://img.skitch.com/20090213-cjiawnwig8udf5a6qf1c45cne8.png)

To install copy `build/clippy.swf` into your MEDIA_ROOT. And put the `clippy`
directory somewhere into your Python path. Add `"clippy"` to your
`INSTALLED_APPS` in your `settings.py`. This should be enough to use the
{% clippy "id" %} template tag in your templates.

The template tag needs the id of the field you want to copy to the clipboard
as a parameter. You can give it an additional parameter describing the
background color to use for the widget.

    {% clippy "someid" "#FF0000" %}

If you don't give a color, the color given in `settings.CLIPPY_BGCOLOR` is
used. It `CLIPPY_BGCOLOR` is not set, `#ffffff` is used as a fall back.

The code comes with a demo application. If you have [pip][2] and
[virtualenv][3] installed, just type `make dependencies runserver`
and go to [http://127.0.0.1:8000/](http://127.0.0.1:8000/) to play with it.


[1]: http://www.djangoproject.com/
[2]: http://pypi.python.org/pypi/pip
[3]: http://pypi.python.org/pypi/virtualenv


Using the Flash Widget without Django
-------------------------------------

The "copy to clipboard" functionality is not reliably available in Javascript
therefore it is implemented in Flash. If you don't use Django, you obviously
can use the Flash widged directly in your HTML code. It can be called like
this:

    <span id="someid">Somevalue</span>
    <object classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000"
            width="110" height="14" id="clippy_someid">
        <param name="movie" value="/mymedia/clippy.swf"/>
        <param name="allowScriptAccess" value="always" />
        <param name="quality" value="high" />
        <param name="scale" value="noscale" />
        <param NAME="FlashVars" value="id=someid">
        <param name="bgcolor" value="#ffffff">
        <embed src="/mymedia/clippy.swf?x=23"
            width="110" height="14" name="clippy" quality="high"
            allowScriptAccess="always"
            type="application/x-shockwave-flash"
            pluginspage="http://www.macromedia.com/go/getflashplayer"
            FlashVars="id=someid" bgcolor="#ffffff" /></object>

The widget understands the following parameters:

* `id` - mandantory. Id from which the 
* copied - text to display after copying. Default is "copied!"
* copyto - text to display before copying. Default is "copy to clipboard"
* callBack - JAvascript function to be called after copying



Compiling the Flash Widget
--------------------------

In order to compile Clippy from source, you need to install the following:

* [haXe](http://haxe.org/)
* [swfmill](http://swfmill.org/)

The haXe code is in `Clippy.hx`, the button images are in `assets`, and the
compiler config is in `compile.hxml`. Make sure you look at all of these to
see where and what you'll need to modify. To compile everything into a final
SWF, type `make flash`.

If that is successful `build/clippy.swf` should be the new flash widged
which you need to copy to your `MEDIA_PATH`.



History
-------

The original clippy code is by Tom Preston-Werner. This version contains
Fixes by Zhang Jinzhu and Kyle Neath. Maximillian Dornseif integrated various
patches and created the Django template Tag. Check the
[GitHub Fork Network][4] to better understand the project history.

[4]: http://github.com/mojombo/clippy/network



License
-------

MIT License (see LICENSE file)
