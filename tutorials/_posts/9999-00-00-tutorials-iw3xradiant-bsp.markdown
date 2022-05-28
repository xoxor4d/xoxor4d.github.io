---
layout:     post
title:      "d3dbsp: Loading and Compiling"
subtitle:   "New Feature"
date:       2022-05-28 16:00:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-d3dbsp/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>
 
<div align="center" markdown="1"> 
__IW3xRadiant__ allows you to compile, load and view d3dbsp files.  
You can toggle between "_radiants world_" and the "_d3dbsp world_", or mix and match however you want. (eg: render bsp but show spawnpoints or fx entities)  
It can be used to quickly iterate map lighting or to place effects. (eg. fx lights/spotlights require a loaded bsp to render)  
</div>

<div class="padding-2l"></div>
## Loading a bsp and compiling it
![](/assets/img/iw3xo-radiant/gif/tut/bsp_loading_compile.gif)

![](/assets/img/iw3xo-radiant/gif/tut/d3dbsp-menubar.jpg# right){: style="margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}

<div class="padding-2l"></div>

> - To load a bsp (can be any) use: _Menubar_ > _d3dbsp_ > _Load d3dbsp .._ 
> - You can also click _Reload d3dbsp_ to automatically load the d3dbsp associated with your currently loaded map
> - Use ![](/assets/img/iw3xo-radiant/ico_bsp_toggle.png){: style="height: 28px; margin-left: 4px"} to toggle to bsp view
> - Use ![](/assets/img/iw3xo-radiant/ico_settings.png){: style="height: 28px; margin-left: 4px"} (below above) to show the bsp compiling menu
    (or use: _Menubar_ > _d3dbsp_ > _Compile Settings .._ )
> - Compiling the bsp (Default F5) will automatically reload it once done

<div class="padding-2l"></div>
