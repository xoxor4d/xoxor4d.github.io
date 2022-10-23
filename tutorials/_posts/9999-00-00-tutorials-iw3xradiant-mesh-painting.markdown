---
layout:     post
title:      "General: Mesh Painter"
subtitle:   "New Feature"
date:       2022-05-28 9:00:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-mesh-painting/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>
 
<div align="center" markdown="1"> 
The mesh painter tool allows you to quickly place ground aligned models and prefabs with random angles and varying size  
by painting on brushes / patches or other prefabs. Add as many objects as you wish and use the per-object settings
to get the result you are after.
</div>

<div class="padding-2l"></div>
<div class="seperator-100p"></div>
<div class="padding-1l"></div>


<div class="padding-1l"></div>
> - Open the mesh painting tool via the menubar -> tools -> Mesh Painter  
> Or via menubar -> view -> toggle -> Mesh Painter
![](/assets/img/iw3xo-radiant/physx/physx_movement.jpg# right){: style="margin-top: -10rem; margin-right: -5rem"}

<div class="padding-2l"></div>
<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/gif/feat_mesh_painter.gif# left){: style="width: 100%; margin-top: -1rem"}

<div class="padding-2l"></div>
![](/assets/img/iw3xo-radiant/tut_meshpainter.jpg# right){: style="margin-top: -3rem; margin-right: -5rem"}
> - Drag and drop models from the model browser or prefabs from the prefab browser  
> into the __list box__ or use the file-browser next to the list box (...)  
> <br>
> - Select an object to adjust the per-object settings and adjust the settings to your liking  
> eg: toggle random size / rotation, set the object weight etc.  
> <br>
> - Use __Toggle Painter__ to go into and out of paint mode. Holding Shift will temporarily  
> disable paint mode so you can select objects to make adjustments via entity properties.  
> <br>
> ### General features:
> - __X:__ delete selected object from the list
> - __S:__ opens a file dialog to save the current list
> - __L:__ opens a file dialog to load a previously saved list from disk
> - __Radius:__ radius of the painter circle
> - __Paint Threshold:__ mouse distance needed for the next paint cycle
> - __Paint Density:__ amount of objects placed per paint cycle  
> <br>
> ### Per Object:
> - __Weight:__ objects will be randomly choosen by their weight. Objects with higher weights have higher chances compared to lower weighted objects - but similar chances to objects with similar weights  
> - __Ground Offset:__ adjust spawn height of the object. Useful if the model origin is not at the bottom

<div class="padding-2l"></div>
<div class="padding-2l"></div>

<div align="center" markdown="1"> 
Tip: Selecting an object (model) from the list box while having the model browser open will preview the selected model in the model browser.
</div>


<div class="padding-2l"></div>
