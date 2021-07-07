---
layout:     post
title:      "Map Exporting"
subtitle:   "In-Depth"
date:       2021-07-03 12:00:00
categorie:  iw3xo
permalink:  /tutorials/iw3xo-mapexport/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" markdown="1"> 
## Overview
<div class="padding-1l"></div>
The map exporting feature heavily depends on the collision drawing feature present in IW3xo.  
This gives you the ability to export only specific brushes or brushes using a material of your choice.
</div>

<div class="padding-2l"></div>
<div class="padding-1l"></div>

## Example: Exporting __All__ brushes
1. Open the [DevGui](/projects/iw3xo/#dvars-devgui) or use [Collision Dvars](/projects/iw3xo/#dvars-collision)
2. Set "r_drawCollision" to anything but 0
3. Set "r_drawCollision_brushDist" to 200 (performance, does not exclude brushes)
4. Set "r_drawCollision_brushAmount" to 0 or max (same thing)
5. Set "r_drawCollision_materialInclude" to all
6. Hit Map Export or use [Mapexport Dvars](/projects/iw3xo/#dvars-mapexport)

<div class="padding-1l" style="margin-bottom: -0.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>

## Example: Exporting all clip-type brushes
1. All of the above
2. Set "r_drawCollision_materialInclude" to clip 
3. Export

<div class="padding-1l"></div>
![](/assets/img/iw3xo/tutorial/mapexport_all_clip.jpg# center)

<div class="padding-1l" style="margin-bottom: -0.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>


## Example: Exporting all brushes using the mantle_on material
1. All of the above
2. Set "r_drawCollision_materialInclude" to none
3. Get the material ID of mantle_on by using "r_drawCollision_materialList"
4. Set "r_drawCollision_material" to the material ID of mantle_on
5. Export

<div class="padding-1l"></div>
![](/assets/img/iw3xo/tutorial/mapexport_material.jpg# center)

<div class="padding-1l" style="margin-bottom: -0.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>

## Example: Exporting a specific section of the map
1. Choose the brush-types you want to include
2. Set "mapexport_selectionMode" to 1
2. Use "mapexport_selectionAdd" to add the first point of the bounding box
3. Move around while facing the direction of your first point to see the bounding box.
4. Use "mapexport_selectionAdd" to add the final point when you are happy with your selection.
5. Export

<div class="padding-1l"></div>
![](/assets/img/iw3xo/tutorial/mapexport_boundingbox.jpg# center)

<div class="padding-1l"></div>