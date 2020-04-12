---
layout:         post
title:          "Call of Duty 4 :: IW3xo"
subtitle:       "a custom client aimed at developers that includes various modifications/additions"
description:    "A custom Call of Duty 4 client with alot of new and useful features for debugging / mod development / gimmicks / movement-tweaks / improved in-game console ..."
date:           2020-04-05 00:00:00
permalink:      /projects/iw3xo/
image:          "/assets/img/iw3xo/thumb.jpg"
status:         "WIP - PUBLIC"
---
<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo/header.jpg"; </script>

<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Quick Links
[GitHub Repository](https://github.com/xoxor4d/iw3xo-dev) :: [Latest Release](https://github.com/xoxor4d/iw3xo-dev/releases) :: [Changelog](https://github.com/xoxor4d/iw3xo-dev/wiki/Changelog) :: [IW3xRadiant](/projects/iw3xo-radiant/)
<div class="padding-2l"></div></div> 

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

<div class="padding-1l"></div>
![](/assets/img/iw3xo/collisionDrawType.jpg) 

<div class="padding-1l"></div>
![](/assets/img/iw3xo/originVelocity.jpg) 

<div class="padding-1l"></div>
![](/assets/img/iw3xo/collisionClip.jpg) 

<div class="padding-1l"></div>
![](/assets/img/iw3xo/collisionClipIndex.jpg) 

<div class="padding-1l"></div>
[![Play](/assets/img/vid-live-link.jpg# left){: style="width: 50%"}](https://www.youtube.com/watch?v=SBqZLfCaRdw) [![Play](/assets/img/vid-map-export.jpg# right){: style="width: 50%"}](https://www.youtube.com/watch?v=UOjiakKrNdk)

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>


<div markdown="1" style="padding-left: 2rem">
# Features ([In-Depth](#in-depth))
<div class="padding-2l"></div>
__Interface__
   + Completely new main menu
   + Improved in-game console (eg. drag / resize with the cursor, console output when not using the fullscreen console, ... )
<div class="padding-2l"></div>
__Rendering__ 
   + Draw debug collision brushes (eg. clip, mantle, multiple, all ...)
   + Draw synchronized radiant brushes
   + Trace origin and/or velocity
   + Built in postfx shaders like SSAO, Cellshading, Toon ...
<div class="padding-2l"></div>
__Radiant Live-Link (requires [IW3xRadiant](/projects/iw3xo-radiant/))__ 
   + Synchronize up to 16 selected radiant-brushes 
   + Synchronized brushes are colliding (requires a prefab within the map)
   + Synchronized worldspawn settings (sundirection, suncolor, sunlight)
   + Synchronize cameras (radiant \-> server, server \-> radiant or both)
<div class="padding-2l"></div>
__Map Exporting__
   + Export brushes (includes tool brushes etc ...)
   + Option to export merged triangles (quads) as patches
   + Option to export leftover unmerged triangles as patches
   + Option to export entities / reflection probes
   + Option to export static models
   + Option to export only certain parts of a map using a bounding box
<div class="padding-2l"></div>
__Movement__ 
   + Dvar tweakable movement types like quake3/cpm or css/surf
   + Dvar tweakable stock movement settings
   + Dvar tweakable origin and/or velocity tracing
<div class="padding-2l"></div>
__FileSystem__
   + Load FastFiles Addons and IWDs on startup
   + Live FastFile loading/reloading
<div class="padding-2l"></div>
__Misc__
   + Dvar cheat/write protection removed
   + Removed the need to precache xmodels (more assets will follow)
   + Manipulate entities with console commands (incomplete)
   + Added the most common gsc function additions like setvelocity(), jumpButtonPressed() ...
   + Fixed mouse lag on some Windows 10 builds (c) Snake
</div>


<div class="padding-1l" style="margin-top: -1.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

![](/assets/img/iw3xo/console01.jpg) 

<div class="padding-1l" style="margin-top: -1.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<a name="in-depth"></a>

<div markdown="1" style="padding-left: 2rem">
# In-Depth Features / Functions / Dvars
<div class="padding-2l"></div>

<div class="highlight-header"><p>In-Game Console</p></div>
{% highlight cpp %}
[Hotkeys]
|-> F1         :: Enable mouse cursor (in-game)
|-> F2         :: Reset Console
|-> Mouse 1 :: Press and hold inputbar to move the console. Press and hold the resize-arrow to resize the console (bottom right)

[Dvars]
|-> xo_con_outputHeight  :: line amount for mini-con output window
|-> xo_con_maxMatches    :: maximum amount of matches to draw
|-> xo_con_padding       :: padding from window borders (default console state (F2))
|-> xo_con_useDepth      :: use depth-preview shader as background for output window
|-> xo_con .....
|-> con_minicon_position :: change position of the minicon
|-> con_minicon .....
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Postfx Shaders</p></div>
{% highlight cpp %}
[Types]
|-> XO_SHADEROVERLAY 1 :: SSAO (dvars : xo_ssao_)
|-> XO_SHADEROVERLAY 2 :: CELLSHADING
|-> XO_SHADEROVERLAY 3 :: OUTLINER (dvars : xo_outliner_)
|-> XO_SHADEROVERLAY 4 :: FULLSCREEN-DEPTH
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Movement</p></div>
{% highlight cpp %}
[Preset Commands]
|-> pm_preset_cs
|-> pm_preset_q3
|-> pm_preset_stock

[Dvars]
|-> pm_debug_traceOrigin    :: trace player origin (multiple options)
|-> pm_debug_traceVelocity  :: trace player velocity (multiple options)
|-> pm_hud_enable           :: disable debug hud with speed/movementtype display
|-> pm_movementType         :: movement TYPES
|-> pm_cpm_ ....            :: q3 settings
|-> pm_cs_ ....             :: cs settings
|-> pm_ ......
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Debug Collision Brushes</p></div>
{% highlight cpp %}
[Dvars]
|-> r_drawCollision                    :: enables collision drawing (multiple options)
|-> r_drawCollision_brushAmount        :: max amount of brushes to draw (starting at index _brushBegin)
|-> r_drawCollision_brushDist          :: max drawing distance
|-> r_drawCollision_brushIndexVisible  :: show clipMap brush indices for each visible debug brush
|-> r_drawCollision_brushIndexFilter   :: ^ only draw specific brushes. Format "index index index" (1 2 3 4 20)
|-> r_drawCollision_brushSorting       :: sort brushes (Z-Fighting; Disabled when using filters) 

|-> r_drawCollision_hud                :: debug hud displaying the current amount of brushes/polygons
|-> r_drawCollision_hud_ ...    

|-> r_drawCollision_material           :: only show brushes with this material index (see below)   
|-> r_drawCollision_materialList       :: print a list of all materials with their index
|-> r_drawCollision_materialInclude    :: preset filters

|-> r_drawCollision_polyLit            :: enable custom-shader usage (unlit fake-lighting)
|-> r_drawCollision_poly ...           :: polygon options
|-> r_drawCollision_line ...           :: line options
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Debug Collision Brushes - Map Exporting</p></div>
{% highlight cpp %}
[Commands]
|-> mapexport                       :: export highlighted brushes + options or bounding box selection
|-> mapexport_selectionAdd          :: adds a point to the bounding box (needs mapexport_selectionMode and 2 points in total)
|-> mapexport_selectionClear        :: reset the bounding box (needs mapexport_selectionMode)

[Dvars]
|-> mapexport_selectionMode         :: export only certain parts of a map by using a bounding box (see commands above)
|-> mapexport_brushEpsilon1         :: brushside generation epsilon 1 (adv. only)
|-> mapexport_brushEpsilon2         :: brushside generation epsilon 2 (adv. only)
|-> mapexport_brushMinSize          :: only export brushes (with more then 6 sides) if their diagonal length is greater then this
|-> mapexport_writeQuads            :: export merged triangles as quads, if enabled
|-> mapexport_writeTriangles        :: export leftover triangles, if enabled
|-> mapexport_writeEntities         :: export map entities, if enabled
|-> mapexport_writeModels           :: export static models, if enabled
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Debug Collision Brushes</p></div>
{% highlight cpp %}
[Commands]
|-> radiant_saveSelection        :: save the current brush selection
|-> radiant_clearSaved           :: clear saved brushes

[Dvars]
|-> radiant_live                 :: enables live-Link
|-> radiant_liveDebug            :: enables live-Link debug prints
|-> radiant_livePort             :: port used for live-Link (has to match radiant)
|-> radiant_syncCamera           :: camera sync modes (radiant->game, game->radiant, both)
|-> radiant_brushColor           :: color of debug brushes created with radiant
|-> radiant_brushCollision       :: enable brush collision (map needs to include prefab <dynamic_collision_bmodels.map>)
|-> radiant_brushLit             :: enable custom-shader usage (unlit fake-lighting)
|-> radiant_brushWireframe       :: enable additional wireframe
|-> radiant_brushWireframeColor  :: color of wireframe
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Misc</p></div>
{% highlight cpp %}
[Commands]
|-> help                   :: link, opens IW3xo Project page
|-> iw3xo_github           :: link, opens IW3xo Github repo
|-> iw3xo_radiant_github   :: link, opens IW3xRadiant Github repo
|-> patchdvars             :: re-register cg_fovscale and snaps to patch their limits

|-> loadzone <zoneName>                   :: load/reload zones (fastfiles)
|-> ent_rotateTo <entityID> <angles vec3> :: rotate any entity 
|-> more entity commands to follow ....
{% endhighlight %}