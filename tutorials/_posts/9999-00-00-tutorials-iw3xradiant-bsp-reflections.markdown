---
layout:     post
title:      "d3dbsp: Generating Reflections"
subtitle:   "New Feature"
date:       2022-05-28 16:00:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-d3dbsp-reflections/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>
 
<div align="center" markdown="1"> 
Can't generate reflections because you've got custom or modified scripts inside your raw folder?  
__IW3xRadiant__ allows you to automatically generate reflections for your map when compiling the map (d3dbsp).  
This eliminates the need to use the __`mp_tool`__ with it's bugs and drawbacks most of you know and 'love'.  

</div>

<div class="padding-2l"></div>
## Generating reflections
![](/assets/img/iw3xo-radiant/gif/tut/bsp_reflections.gif)

> - You don't have to do anything besides making sure that you have checked 'Automatically compile reflections when building bsp'
> - Compile your bsp and reflections will be generated automatically  
> ( You can also trigger the process manually by using the 'Generate Reflections' button. Note that its using the reflection probe position data thats inside the compiled bsp, so make sure your bsp is up-to-date)


<div class="padding-2l"></div>
