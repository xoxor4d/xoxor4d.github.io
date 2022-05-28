---
layout:     post
title:      "General: Live Link"
subtitle:   "New Feature"
date:       2022-05-28 17:00:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-livelink/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" markdown="1"> 
The Live-Link feature allows you to synchronize brushes with working collision, camera and worldspawn settings between [[IW3xRadiant]](https://github.com/xoxor4d/iw3xo-radiant) and [[IW3xo]](https://github.com/xoxor4d/iw3xo-dev).  
This is especially useful for CoDJumper / Deathrun maps as you can quickly iterate and change bounces, platforms .. you get the point.

</div>


<div class="padding-1l"></div>
<div class="padding-2l"></div>
![](/assets/img/iw3xo/gif/feat_livelink.gif) 

<div class="padding-2l"></div>
<div class="padding-2l"></div>

## Setup

* Place the __`dynamic_collision_bmodels.map`__ prefab found in __`map_source\prefabs\_iw3xo`__ into your map. (Preferably into the sky)
![](/assets/img/iw3xo-radiant/tut_livelink_prefab.jpg# right){: style="width: 42%; margin-top: 3rem; margin-right: -1rem"}
* Compile your maps bsp and fastfiles
* Keep radiant open and launch IW3xo.   
Make sure that the following dvars are enabled and are matching radiant's:

{% highlight cpp %}
|-> radiant_live        :: enables live-Link
|-> radiant_livePort    :: port used for live-Link (has to match radiant)
{% endhighlight %}

* Load up your map. You should now see such a print in radiant's console: 
![](/assets/img/iw3xo-radiant/tut_livelink_radiant_console.jpg){: style="margin-top: 2rem; margin-bottom: 2rem"}

* IW3xo should report the same, followed by some initialization prints where it searches for the __`dynamic_collision_bmodels.map`__ prefab. (Used for collisions)

![](/assets/img/iw3xo-radiant/tut_livelink_camera_sync.jpg){: style="width: 42%; margin-top: 0rem; margin-left: 4rem"} 
<p align="right" markdown="1">
	^ use the devgui found in iw3xo or the __`radiant_syncCamera`__ dvar to change the way camera synchronization is handled.<br>
</p>

<div class="padding-2l"></div>
## Saving your selection
![](/assets/img/iw3xo/gif/feat_livelink_save_selection.gif) 

> - Select everything you want (eg. start and end platform)
> - Open the devgui and select __Save Current Selection__ (you could now edit the bounce inbetween without loosing the start and end platform)
> - Use __Clear Saved Selection__ to clear synced brushes

<div class="padding-2l"></div>