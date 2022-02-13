---
layout:         post
title:          "Call of Duty 4 :: IW3xRadiant"
subtitle:       "A Call of Duty 4 Radiant Modification using ImGui"
description:    "A CoD4 Radiant Modification built to be used with IW3xo. Live-Link between CoD4 and Radiant. ImGui UI, Brush/Camera synchronization, Effects, Filmtweaks, Fog, Reflections ..."
date:           2022-02-01 00:00:00
permalink:      /projects/iw3xo-radiant/
image:          "/assets/img/iw3xo-radiant/thumb.jpg"
status:         "WIP - PUBLIC"
---
<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>

<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -4rem" markdown="1">
#### Quick Links
[[GitHub Repository]](https://github.com/xoxor4d/iw3xo-radiant) :: [[Latest Release]](https://github.com/xoxor4d/iw3xo-radiant/releases) :: [[IW3xo]](/projects/iw3xo/)  
[[Installation]](#install) :: [[Using Live Link]](#tut-livelink) :: [[Features / Buttons]](#tut-general)
</div>

<div class="padding-1l"></div>
<h1 align="center">IW3xRadiant - A Call of Duty 4 Radiant Modification using ImGui</h1>
<div align="center" style="margin-top: -2.5rem"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -1.5rem"></div>

<p align="center">
This project is aimed at developers and includes various modifications/additions and was initially built to be used with IW3xo. <br>
Running IW3xRadiant and IW3xo enables a live-link between CoD4 and Radiant. You can, however, just use it as a direct replacement for stock radiant.
</p>

<div class="padding-2l"></div>

### Completely revamped user interface with docking, tabs, saved layouts customizable toolbar and more (Dear ImGui)
![](/assets/img/iw3xo-radiant/gif/feat_ui.gif) 

<div class="padding-1l"></div>
### Play and export createFX files right from within radiant
![](/assets/img/iw3xo-radiant/gif/radiant_effect_leaves.gif) 

<div class="padding-1l"></div>
### Custom sun shaders with support for normalmapping, specular highlights, reflections and fog
![](/assets/img/iw3xo-radiant/gif/feat_fakesun_settings.gif) 

<div class="padding-1l"></div>
### Model previewer - drag and drop models directly into the scene
![](/assets/img/iw3xo-radiant/gif/feat_modelpreview.gif) 

<div class="padding-1l"></div>
### Live-link to synchronize selected brushes (with collision) and worldspawn settings between CoD4 and Radiant 
![](/assets/img/iw3xo-radiant/gif/feat_livelink_brushes_cam.gif) 

<div class="padding-1l"></div>
### Filmtweak support
![](/assets/img/iw3xo-radiant/gif/feat_filmtweaks.gif) 

<div class="padding-1l"></div>
<div align="center" style="margin-top: 2.5rem"><div class="seperator-100p"></div></div>

<div markdown="1" style="padding-left: 2rem">
__Interface / General__
   + Completely revamped user interface with docking, tabs, saved layouts and more (Dear ImGui)
   + 3D guizmo to preciously manipulate entities and brushes from the camera window (ImGuizmo)
   ![](/assets/img/iw3xo-radiant/feat_guizmo.jpg# right){: style="width: 42%; margin-top: 1rem; margin-right: -1rem"}
   + Preview xmodels and drag them directly into the scene using the model previewer
   + Realtime viewports (adjust FPS per Viewport)
   + Save and load dvars to/from config
   + Hotkey editor
   + Color editor 
   + Toolbar editor
   + Better surface / entity property editor
   + New preferences menu with categories
   + Grid Window: Zoom to cursor
   + Increased undo limit (512)
   + Texture window toolbar with quick filtering
   + Console with dvar support (including dvar suggestions and autocomplete)
   + External console that runs on startup showing the initialization process
   
<div class="padding-2l"></div>
Gameview - hide all tool entities and textures with a single click
![](/assets/img/iw3xo-radiant/feat_gameview.jpg) 

<br>
<br>
__Effects__
	![](/assets/img/iw3xo-radiant/gif/radiant_effect_fire.gif# right){: style="width: 32%; margin-top: 3rem; margin-right: -1rem"}
   + New entity: __`fx_origin`__
   + Play individual effects assigned to __`fx_origin`__ entites right within the editor
   + Effects directly react to translations and rotations of their __`fx_origin`__ entity
   + Play, play-repeat, pause and stop effects from the camera toolbar
   + Adjust global effect timescale and enable debugging options using the effects settings menu
   + Generate createfx / loadfx files for all fx_origin entities on the currently loaded map
   + Future Goal - edit effects right within radiant
   + Future Goal - play effects of multiple __`fx_origin`__ entites at once
   + Future Goal - physics

<div class="padding-2l"></div>
![](/assets/img/iw3xo-radiant/gif/feat_effects_spawn.gif) 

<br>
<br>
__Rendering__
   + Option to disable patch backface wireframe
   + Option to disable entity origin boxes
   + Active light preview no longer darkens the rest of the map
   + Selecting a brush with sunlight-preview enabled no longer darkens the rest of the map
   + Disabled sunlight-preview shadows (++FPS)

<div class="padding-2l"></div>
Custom lighting shader with normal-mapping, specular highlights, reflections and fog
![](/assets/img/iw3xo-radiant/feat_fakesun_fog.jpg) 
<div class="padding-1l"></div>
![](/assets/img/iw3xo-radiant/gif/feat_fakesun_settings_man.gif) 

![](/assets/img/iw3xo-radiant/collisionDrawType.jpg# left) ![](/assets/img/iw3xo-radiant/collisionClip.jpg# right) 

<br>
<br>
__Live-Link__
   + Synchronize selected brushes (with collision) 
   + Synchronize radiant and game camera
   + Synchronize worldspawn settings

<div class="padding-2l"></div>
![](/assets/img/iw3xo-radiant/link03.jpg) 
</div>


<div class="padding-1l"></div>
<div align="center" style="margin-top: 2.5rem; margin-bottom: 2.5rem"><div class="seperator-100p"></div></div>


<a name="install"></a>
## Installation

Download the [Latest Release](https://github.com/xoxor4d/iw3xo-radiant/releases) and unzip the contents into your CoD4 root directory.  
Go into the bin folder and open __`IW3xRadiant.exe`__. You'll be asked to open a project file. Go ahead and select __`iw3xradiant.prj`__ found in _root/bin_.  
<p align="right">
	(IW3xRadiant requires the CoD4 Modtools, obviously)<br>
</p>


<div class="padding-1l"></div>
<div align="center" style="margin-top: 2.5rem; margin-bottom: 2.5rem"><div class="seperator-100p"></div></div>

<a name="tut-livelink"></a>
## Using Live-Link

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
<p align="right">
	^ Use IW3xo's devgui or the __`radiant_syncCamera`__ dvar to change the way camera synchronization is handled.<br>
</p>

<div class="padding-1l"></div>
<div align="center" style="margin-top: 2.5rem; margin-bottom: 2.5rem"><div class="seperator-100p"></div></div>

<a name="tut-general"></a>
## Features / Buttons explained

![](/assets/img/iw3xo-radiant/ico_gameview.png){: style="width: 4%; margin-top: 1rem; margin-bottom: 1rem; margin-right: 1rem"} __`Gameview`__ - hide all tool entities and textures with a single click (__`Menubar > View > Toggle > Game View`__)  

![](/assets/img/iw3xo-radiant/ico_fakesun.png){: style="width: 4%; margin-top: 1rem; margin-bottom: 1rem; margin-right: 1rem"} __`Fake Sun Preview`__ - toggle custom sunlight shader (__`Menubar > Renderer > Render Method > Fake Sun Preview`__)  

![](/assets/img/iw3xo-radiant/ico_fog.png){: style="width: 4%; margin-top: 1rem; margin-bottom: 1rem; margin-right: 1rem"} __`Fog`__ - toggle fog (requires custom sunlight shader to be active)  

![](/assets/img/iw3xo-radiant/ico_filmtweaks.png){: style="width: 4%; margin-top: 1rem; margin-bottom: 1rem; margin-right: 1rem"} __`Filmtweaks`__ - toggle filmtweaks  

![](/assets/img/iw3xo-radiant/ico_settings.png){: style="width: 4%; margin-top: 1rem; margin-bottom: 1rem; margin-right: 1rem"} __`Settings`__ - opens advanced sunlight, filmtweaks and effects settings  

![](/assets/img/iw3xo-radiant/ico_cubic_clip.png){: style="width: 4%; margin-top: 1rem; margin-bottom: 1rem; margin-right: 1rem"} __`Cubic Clipping`__ - reduce drawing distance. Distance can be adjusted under __`Menubar > Renderer > Cubic Scale`__  

![](/assets/img/iw3xo-radiant/ico_undock.png){: style="width: 4%; margin-top: 1rem; margin-bottom: 1rem; margin-right: 1rem"} __`Undock Window`__ - triangle that appears on the upper-left corner of a fully docked window. Single click shows tab bar. Click-drag to undock the window.