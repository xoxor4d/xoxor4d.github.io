---
layout:     post
title:      "Effects: Place and play"
subtitle:   "New Feature"
date:       2022-05-28 12:00:00
categorie:  iw3xradiant
permalink:  /tutorials/iw3xradiant-using-effects/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>
 
<div align="center" markdown="1"> 
__IW3xRadiant__ allows you to play and [edit](/tutorials/iw3xradiant-effects-editor) effects right inside the editor.  
This drastically improves the effect workflow as you can see changes happening in realtime without having to recompile and reloading your map in-game.  
It can also generate so-called [createfx](/tutorials/iw3xradiant-createfx) files that are automatically loaded by the game.
</div>

<div class="padding-2l"></div>
## Placing and playing effects
![](/assets/img/iw3xo-radiant/gif/tut/efx_spawing.gif) 


> - Create an __fx_origin__ entity by right clicking the grid window > _Create Entity_ > _fx_origin_  
> - Use the play, pause and stop buttons within the camera toolbar (you can add these buttons to the main toolbar via the toolbar editor)
> - Effects get their  _origin_ and _angles_ from the fx_origin entity
> - (It's best to place fx_origin entities into your main .map file and not into prefabs)

<a name="efxdef"></a>
<div class="padding-2l"></div>
## Changing the effect definition
![](/assets/img/iw3xo-radiant/gif/tut/efx_def_changing.gif) 


> - With the __fx_origin__ selected, open up the entity properties (Default __N__)
> - Open the filedialog using the " __..__ " button next to the _fx_ key-value-pair
> - Select an .efx file of your choice and hit play

<div class="padding-2l"></div>