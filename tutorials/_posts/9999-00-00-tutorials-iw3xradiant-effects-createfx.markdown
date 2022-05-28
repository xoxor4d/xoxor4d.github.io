---
layout:     post
title:      "Effects: Generate CreateFX files"
subtitle:   "New Feature"
date:       2022-05-28 10:00:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-createfx/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>
 
<div align="center" markdown="1"> 
__IW3xRadiant__ allows you to [play and place](/tutorials/iw3xradiant-using-effects) effects right inside the editor.  
It can generate so-called __createfx__ files that are automatically loaded by the game.
</div>

<div class="padding-2l"></div>
## Generating CreateFX files
![](/assets/img/iw3xo-radiant/gif/tut/efx_createfx1.jpg# left){: style="height: 440px; margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
![](/assets/img/iw3xo-radiant/gif/tut/efx_createfx2.jpg# right){: style="height: 440px; margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}

> - _Menubar_ > _File_ > _Generate File_ > _Createfx_ 
> - This will generate createfx files using data off all fx_origins present on your map (you don't need to select them)
> - Radiant will save the generated files to: _`cod4/bin/IW3xRadiant/createfx`_

![](/assets/img/iw3xo-radiant/gif/tut/efx_createfx3.jpg# right){: style="margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}

<div class="padding-2l"></div>
<div class="padding-2l"></div>
<div class="padding-2l"></div>

## Using CreateFX files on your map

> - Copy paste the file: __`mp_MAPNAME_fx.gsc`__ from __`cod4/bin/IW3xRadiant/createfx`__ &ensp; to &ensp; __`cod4/raw/maps/mp/`__ (next to your maps gsc)
> - Copy paste the file: __`mp_MAPNAME_fx.gsc`__ from __`cod4/bin/IW3xRadiant/createfx/createfx`__ &ensp; to &ensp; __`cod4/raw/maps/createfx/`__

<div class="padding-1l"></div>

<div class="highlight-header"><p>Add the files to your map's zone file</p></div>
{% highlight cpp %}
rawfile,maps/mp/mp_MAPNAME_fx.gsc
rawfile,maps/createfx/mp_MAPNAME_fx.gsc
{% endhighlight %}

<div class="padding-1l"></div>

<div class="highlight-header"><p>Add the following to your maps gsc</p></div>
{% highlight xxx %}
main()
{
	/* ... */

	maps\mp\_load::main();
	maps\mp\mp_MAPNAME_fx::main(); // <-

	/* ... */
}
{% endhighlight %}

<div class="padding-2l"></div>