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
[[Installation]](#install) :: [[Using Live Link]](#tut-livelink) :: [[Features / Buttons]](#tut-general) :: [[Noticeable Changes]](#tut-general)
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
   + play, edit and export effects as createFx files right from within radiant (makes effectsEd almost obsolete)
   + switch / scale / place the individual windows however you want
   + preview xmodels and drag them directly into the scene using the model previewer
   + live link (sync. brushes (with collision), camera and worldspawn settings between cod4 and radiant)
   + custom lighting shader with normal-mapping, specular highlights, reflections and fog
   + ability to limit shadow drawing distance when using stock sunpreview (++FPS)
   + filmtweak support
   + render actual water instead of case-textures
   ![](/assets/img/iw3xo-radiant/feat_guizmo.jpg# right){: style="width: 42%; margin-top: 1rem; margin-right: -1rem"}
   + guizmo to manipulate entities and brushes from within the camera window
   + high poly xmodel's no longer crash radiant
   + realtime viewports
   + better surface / property editor
   + context aware grid and camera context menus with QoL features
   + better vertex edit dialog
   + zoom to cursor
   + editable toolbars, hotkeys, colors (all saved)
   + new file dialogs with working default paths
   + texture window toolbar for quick filtering
   + rope/wire generator
   + sun direction visualizer
   + a proper console with dvar support (incl. dvar suggestions and autocomplete)
   + increased undo limit
   + print parsed entity and brush num on map load making it easier to find issues in map files (off by default)
   + alot of QOL features

   
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
   + Edit effects right within radiant (EffectsEd)
   + Future Goal - play effects of multiple __`fx_origin`__ entites at once
   + Future Goal - physics

<br>

<p float="left">
  <img src="/assets/img/iw3xo-radiant/fxedit_01.jpg" width="40%" />
  <img src="/assets/img/iw3xo-radiant/fxedit_03.jpg" width="40%" align="right" /> 
</p>

<br>

![](/assets/img/iw3xo-radiant/fxedit_02.jpg) 

<div class="padding-2l"></div>

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

<div align="center" markdown="1">
[![build-develop](https://img.shields.io/github/workflow/status/xoxor4d/iw3xo-radiant/Build/develop?logo=github&label=nightly-develop)](https://nightly.link/xoxor4d/iw3xo-radiant/workflows/build/develop/Debug%20binaries.zip)&ensp;
[![build-release](https://img.shields.io/github/workflow/status/xoxor4d/iw3xo-radiant/Build/develop?logo=github&label=nightly-release)](https://nightly.link/xoxor4d/iw3xo-radiant/workflows/build/develop/Release%20binaries.zip)&ensp;
nightly builds - develop branch ( download and install the [latest release](https://github.com/xoxor4d/iw3xo-radiant/releases) before using nightly's )
</div>

<br>

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

<div class="padding-1l"></div>
<div align="center" style="margin-top: 2.5rem; margin-bottom: 2.5rem"><div class="seperator-100p"></div></div>

<a name="tut-noticeable-changes"></a>
## Most noticeable changes / differences compared to stock radiant

- The hotkey for increase / decrease grid (curve patch subdivision) was changed and is now __`SHIFT+9/0`__ by default.  
Function can also be found under __`Menubar > Patch > Inc/Dec Subdevision`__  