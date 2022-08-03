---
layout:     post
title:      "Nvidia PhysX: Prefabs"
subtitle:   "New Feature"
date:       2022-05-28 9:20:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-physx-prefabs/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>
 
<div align="center" markdown="1"> 
The Nvidia PhysX integration allows for physics simulations on [physics-enabled effect-models](/tutorials/iw3xradiant-physx-effects)     
or for __prefabs__ (more precisely, the _convex hull formed by all brushes within the prefab_)
</div>

<div class="padding-2l"></div>
<div class="seperator-100p"></div>
<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/physx/physx_generate_actors.jpg# right){: style="margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
<div class="padding-1l"></div>
> - Click the __effects-cog__ found within the camera toolbar
> - Select all the prefabs you want to turn into dynamic prefabs <br> <br>
> - Click __Generate Static Collision__ which will cook and prepare the world collision using <br> all non-selected radiant brushes / patches and prefabs (__excludes__ selected stuff) <br> <br>
> - Click __Convert Prefabs to PhysX actors__ while still having your prefabs selected
> - Use Play / Pause / Repeat <br> (__NOTE__ no Undo's are created so use pause/repeat to reset your objects back to their initial state)

<div class="padding-2l"></div>
<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/physx/prefab_physics_01.gif# left){: style="width: 100%; margin-top: -1rem"}

<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/physx/prefab_physics_02.gif# left){: style="width: 100%; margin-top: -1rem"}

<div class="padding-2l"></div>
<div class="padding-2l"></div>
