---
layout:     post
title:      "Nvidia PhysX: Effects"
subtitle:   "New Feature"
date:       2022-05-28 9:30:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-physx-effects/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>
 
<div align="center" markdown="1"> 
__IW3xRadiant__ allows you to play and [edit](/tutorials/iw3xradiant-effects-editor) effects right inside the editor.  
<br>
The Nvidia PhysX integration allows for physics simulations on physics-enabled effect-models   
(a feature the original effects editor __`EffectsEd`__ did not support) 
</div>

<div class="padding-2l"></div>
<div class="seperator-100p"></div>
<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/physx/fx_enable_phys.jpg# right){: style="margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
<div class="padding-2l"></div>
> - Open the effects editor and go to the __Physics__ tab
> - Make sure that both checkboxes __Enable Physics__ & __Enable simulation__ are checked


<div class="padding-2l"></div>

![](/assets/img/iw3xo-radiant/physx/fx_model_visuals.jpg# right){: style="margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
<div class="padding-2l"></div>
> - Go to the __Visuals__ tab
> - Make sure that your elem is of type __Model__ with atleast one valid xmodel 


<div class="padding-2l"></div>
<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/physx/physx_generate_actors.jpg# right){: style="margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
<div class="padding-2l"></div>
> - Go back to the __Physics__ tab and open the __PhysX Settings__ <br> (alternatively, click the effects-cog within the camera toolbar) <br> <br>
> - Click __Generate Static Collision__ which will cook static meshes using all radiant brushes and patches <br> (__excludes__ selected brushes / patches - this might take a few seconds) <br> <br>
> - Select your fx_origin, hit play and enjoy

<div class="padding-2l"></div>
<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/physx/fx_physics_preview.gif# left){: style="width: 100%; margin-top: -1rem"}

<div class="padding-2l"></div>

### Turn spawned effect models into misc_models ( Pause your effect and hit `Convert FX PhysX actors to misc_models` )
![](/assets/img/iw3xo-radiant/physx/fx_convert_to_misc_models.gif# left){: style="width: 100%; margin-top: -1rem"}

<div class="padding-2l"></div>

## Debug visualisation and custom collision shapes

![](/assets/img/iw3xo-radiant/physx/physx_debug_visualization.jpg# right){: style="margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
<div class="padding-1l"></div>
> - Enable debug visuals within the PhysX settings menu
> - __Draw shapes__ renders the actual collision mesh
> - __Draw aabbs__ renders the bounding box 
> - __Draw contacts__ renders collision contact points (use without shapes or aabbs)
> - The __Vis. Box Size__ parameter defines the maximum distance at which to draw debug data

<div class="padding-2l"></div>

![](/assets/img/iw3xo-radiant/physx/fx_sphere_shape_debug_vis.gif# left){: style="width: 100%; margin-top: -1rem"}

> - Collision meshes used by effect models are defined by their total bounds (a cube) which might not produce the desired result
> - The PhysX settings menu has an option to change the collision mesh size or overall shape from a cube to a sphere or a custom shape
> - __Custom Shape__: select a brush you want to use as your collision mesh and hit __use selected brush as shape__

<div class="padding-1l"></div>

![](/assets/img/iw3xo-radiant/physx/fx_custom_shape.gif# left){: style="width: 100%; margin-top: -1rem"}

<div class="padding-2l"></div>
<div class="padding-2l"></div>