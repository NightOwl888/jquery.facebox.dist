[![jquery-facebox MyGet Build Status](https://www.myget.org/BuildSource/Badge/jquery-facebox?identifier=1845d11b-3fcd-45c5-98e8-0b90d5b796cb)](https://www.myget.org/)

# Facebox

Facebox is a jQuery-based, Facebook-style lightbox which can display images, divs, or entire remote pages.

[See it in action](http://defunkt.github.com/facebox/).

![Sample Image](http://share.kyleneath.com/captures/Facebox_1.2-20100417-190352.jpg)

## Compatibility

This release relies on a lot of advanced CSS techniques (box-shadow, border-radius, RGBA). That being said, it's compatible with many browsers.

* **Safari 4**
* **Webkit Nightlies** (Chromium, Chrome) as of 4/17/10
* **Firefox 3.5**
* **IE8** (degraded experience)
* **IE7** (degraded experience)
* IE6 - I just don't care
* Opera - I just don't care

Prerequisites
---------------------------------
- [jQuery](http://jquery.com) (>= 1.4.2)

> If you are using a [Package Manager](#package-managers), these dependencies will be installed automatically, but depending on your environment you may still need to add references to them manually.

## Download & Installation
There are several different ways to get the code. Some examples below:

#### CDN
Dirty Forms is available over jsDelivr CDN and can directly included to every page.
```HTML
<script type="text/javascript" src="//cdn.jsdelivr.net/jquery.facebox/1.4.1/jquery.facebox.min.js"></script>
```

jsDelivr also supports [on-the-fly concatenation of files](https://github.com/jsdelivr/jsdelivr#load-multiple-files-with-single-http-request), so you can reference only 1 URL to get jQuery and jquery.facebox in one request.
```HTML
<script type="text/javascript" src="//cdn.jsdelivr.net/g/jquery@1.11.3,jquery.facebox@1.4.1"></script>
```

#### Self-Hosted
Download and save one of two available files to include Dirty Forms to your page, either the [latest distribution](https://raw.githubusercontent.com/NightOwl888/jquery.facebox.dist/master/jquery.facebox.js) or the [latest minified](https://raw.githubusercontent.com/NightOwl888/jquery.facebox.dist/master/jquery.facebox.min.js) version.
```HTML
<script type="text/javascript" src="jquery.facebox.min.js"></script>
```

You can also conveniently get all of the latest Dirty Forms files in one [Zip Download](https://github.com/NightOwl888/jquery.facebox.dist/archive/master.zip).

#### Package Managers
Facebox is even available through [NPM](http://npmjs.org), [Bower](http://bower.io), and [NuGet](https://www.nuget.org/). Just use one of the following commands below to install the helper, including all dependencies.

[![NPM version](https://badge.fury.io/js/jquery.facebox.svg)](http://www.npmjs.org/package/jquery.facebox)
[![Bower version](https://badge.fury.io/bo/jquery.facebox.svg)](http://bower.io/search/?q=jquery.facebox)
[![NuGet version](https://badge.fury.io/nu/jquery.facebox.svg)](https://www.nuget.org/packages/jquery.facebox/)

[![NPM](https://nodei.co/npm/jquery.facebox.png?compact=true)](https://nodei.co/npm/jquery.facebox/)
```
// NPM
$ npm install jquery.facebox

// Bower
$ bower install jquery.facebox

// NuGet
PM> Install-Package jquery.facebox
```

## SourceMaps

A [SourceMap](https://docs.google.com/document/d/1U1RGAehQwRypUTovF1KRlpiOFze0b-_2gc6fAH0KY0k/edit?hl=en_US&pli=1&pli=1) file is also available via CDN or your favorite package manager.

####CDN

```HTML
<script type="text/javascript" src="//cdn.jsdelivr.net/jquery.facebox/1.4.1/jquery.facebox.min.js.map"></script>
```

#### Package Managers

NPM or Bower will install the file into the destination directory.

```
jquery.facebox.min.js.map
```

For NuGet, this file is not included in the package, but you can get it from [here](https://github.com/NightOwl888/jquery.facebox.dist/blob/master/jquery.facebox.min.js.map) if you really need it.


## Usage

Include the [prerequisites](#prerequisites) and facebox in the page. Tell facebox where you've put `src/loading.gif` and `src/closelabel.png`

    $.facebox.settings.closeImage = '/images/facebox/closelabel.png'
    $.facebox.settings.loadingImage = '/images/facebox/loading.gif'

> NOTE: The default is to download the images via jsDelivr CDN, so be sure to update these settings if you want to host the images locally.

Calling facebox() on any anchor tag will do the trick, it's easier to give your Faceboxy links a rel="facebox"  and hit them all onDomReady.

    jQuery(document).ready(function($) {
      $('a[rel*=facebox]').facebox()
    })

Any anchor links with `rel="facebox"` with now automatically use facebox:

    <a href="#terms" rel="facebox">Terms</a>
      Loads the #terms div in the box

    <a href="terms.html" rel="facebox">Terms</a>
      Loads the terms.html page in the box

    <a href="terms.png" rel="facebox">Terms</a>
      Loads the terms.png image in the box


### Using facebox programmatically

    jQuery.facebox('some html')
    jQuery.facebox('some html', 'my-groovy-style')

The above will open a facebox with "some html" as the content.

    jQuery.facebox(function($) {
      $.get('blah.html', function(data) { $.facebox(data) })
    })

The above will show a loading screen before the passed function is called,
allowing for a better ajaxy experience.

The facebox function can also display an ajax page, an image, or the contents of a div:

    jQuery.facebox({ ajax: 'remote.html' })
    jQuery.facebox({ ajax: 'remote.html' }, 'my-groovy-style')
    jQuery.facebox({ image: 'stairs.jpg' })
    jQuery.facebox({ image: 'stairs.jpg' }, 'my-groovy-style')
    jQuery.facebox({ div: '#box' })
    jQuery.facebox({ div: '#box' }, 'my-groovy-style')

### Events

Want to close the facebox?  Trigger the `close.facebox` document event:

    jQuery(document).trigger('close.facebox')

Facebox also has a bunch of other hooks:

* `loading.facebox`
* `beforeReveal.facebox`
* `reveal.facebox` (aliased as `afterReveal.facebox`)
* `init.facebox`
* `afterClose.facebox`  (callback after closing `facebox`)

Simply bind a function to any of these hooks:

    $(document).bind('reveal.facebox', function() { ...stuff to do after the facebox and contents are revealed... })

### Customization

You can give the facebox container an extra class (to fine-tune the display of the facebox) with the facebox[.class] rel syntax.

    <a href="remote.html" rel="facebox[.bolder]">text</a>

## Contact & Help

If you have questions, feel free to ask on the [Google Groups Mailing List](http://groups.google.com/group/facebox/). Alternatively if you find a bug, you can [open an issue](http://github.com/defunkt/facebox/issues).
