---
layout:         post
title:          "Call of Duty 4 :: IW3xRadiant"
subtitle:       "A Call of Duty 4 Radiant Modification using ImGui"
description:    "A CoD4 Radiant Modification built to be used with IW3xo. Live-Link between CoD4 and Radiant. ImGui UI, Brush/Camera synchronization, Effects, Filmtweaks, Fog, Reflections ..."
date:           2022-05-28 00:00:00
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
[[GitHub Repository]](https://github.com/xoxor4d/iw3xo-radiant) :: [[Latest Release]](https://github.com/xoxor4d/iw3xo-radiant/releases) :: [[IW3xo]](/projects/iw3xo/)  :: [[Installation]](#install) :: [[Usage Tutorials]](/tutorials#iw3xradiant)
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
### Play, create, edit and export createFX files right from within radiant
![](/assets/img/iw3xo-radiant/gif/feat_efx_editor.gif) 

<a name="d3dbsp-prev"></a>
<div class="padding-1l"></div>
### D3DBSP loading and compilation - quickly toggle between the actual in-game view and radiants _world_
![](/assets/img/iw3xo-radiant/gif/feat_bsp_compiling.gif) 

<div class="padding-1l"></div>
### Custom sun shaders with support for normalmapping, specular highlights, reflections and fog (radiant _world_)
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
__Feature List__
   + completely revamped user interface with docking, tabs, saved layouts and more (Dear ImGui)
   + [play](/tutorials/iw3xradiant-using-effects) && [edit / create](/tutorials/iw3xradiant-effects-editor) && [export effects as CreateFX](/tutorials/iw3xradiant-createfx) files right from within radiant (__makes effectsEd completely obsolete__)
   + [d3dbsp loading](/tutorials/iw3xradiant-d3dbsp) and bsp/light compilation from within radiant
   + [live link](/tutorials/iw3xradiant-livelink) (sync. brushes (with collision), camera and worldspawn settings between cod4 and radiant)   
   + 3D guizmo to precisely manipulate entities and brushes from the camera window (ImGuizmo)
   + preview xmodels and drag them directly into the scene using the model previewer
   + custom lighting shader with normal-mapping, specular highlights, reflections and fog
   + ability to limit shadow drawing distance when using stock sunpreview (++FPS)
   + filmtweak support
   + render actual water instead of case-textures
   ![](/assets/img/iw3xo-radiant/feat_guizmo.jpg# right){: style="width: 42%; margin-top: 1rem; margin-right: -1rem"}
   + increased asset limits to allow high poly models
   + realtime viewports
   + context aware grid and camera context menus with QoL features
   + better surface / property editor
   + better vertex edit dialog
   + zoom to cursor
   + editable toolbars, hotkeys, colors
   + new file dialogs with working default paths
   + texture window toolbar for quick filtering
   + rope/wire generator
   + sun direction visualizer
   + a proper console with dvar support (incl. dvar suggestions and autocomplete)
   + increased undo limit
   + print parsed entity and brush num on map load making it easier to find issues in map files (off by default)
   + bo3 tool textures (optional)
   + [stamp prefabs](/tutorials/iw3xradiant-prefab) 
   + [create prefab from selection](/tutorials/iw3xradiant-prefab) 
   + terrain patch thickening
   + [extrude selected brush to other brush faces](/tutorials/iw3xradiant-brush-face-extending) 
   + .... + alot more QOL features
   
<div class="padding-2l"></div>
Gameview - hide all tool entities and textures with a single click
![](/assets/img/iw3xo-radiant/feat_gameview.jpg) 

<br>
<br>
__Effects__
	![](/assets/img/iw3xo-radiant/gif/radiant_effect_fire.gif# right){: style="width: 32%; margin-top: 3rem; margin-right: -1rem"}
   + New entity: __`fx_origin`__
   + [Play](/tutorials/iw3xradiant-using-effects) individual effects assigned to __`fx_origin`__ entites right within the editor
   + Effects directly react to translations and rotations of their __`fx_origin`__ entity
   + Play, play-repeat, pause and stop effects from the camera toolbar
   + [Edit and create](/tutorials/iw3xradiant-effects-editor) effects right within radiant (EffectsEd)
   + Ability to step through the effect frame by frame
   + Adjust global effect timescale and enable debugging options using the effects settings menu
   + Generate createfx / loadfx files for all fx_origin entities on the currently loaded map
   + Future Goal - play effects of multiple __`fx_origin`__ entites at once
   + Future Goal - physics

<br>

![](/assets/img/iw3xo-radiant/fxedit_02.jpg# left){: style="width: 75%; margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
![](/assets/img/iw3xo-radiant/fxedit_03.jpg# right){: style="height: 800px; margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}

<div class="padding-2l"></div>

<br>
<br>
__Rendering__
   + [[d3dbsp preview]](#d3dbsp-prev) with almost all rendering features found in cod4 
     + logic to quickly toggle between radiant/bsp 'worlds'
	 + bsp and light compiling options
	 + automatically reload bsp after compilation
	 + effect lights/spotlights visible with loaded bsp
	 + alot of stock iw3-engine debug dvars that are stripped from cod4 but available in radiant

   + Filmtweaks
   + Fog
   + Specular and normalmapping
   + Option to disable patch backface wireframe
   + Option to disable entity origin boxes
   + Active light preview no longer darkens the rest of the map
   + Selecting a brush with sunlight-preview enabled no longer darkens the rest of the map
   + Sunlight-preview shadows can be disabled or clipped by distance (++FPS)
   + Sundirection debug visualizer

<br>
<br>

<div class="padding-2l"></div>
Custom lighting shader with normal-mapping, specular highlights, reflections and fog
![](/assets/img/iw3xo-radiant/feat_fakesun_fog.jpg) 
<div class="padding-1l"></div>
![](/assets/img/iw3xo-radiant/gif/feat_fakesun_settings_man.gif) 

<br>
<br>
__Live-Link__
   + [Synchronize selected brushes](/tutorials/iw3xradiant-livelink) (with collision) 
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

If you want the newest and latest but potentially unstable build, get a nightly. Follow the second paragraph and get an actual release otherwise.

<br>

[![build-develop](https://img.shields.io/github/workflow/status/xoxor4d/iw3xo-radiant/Build-Debug/develop?logo=github&label=nightly-develop)](https://nightly.link/xoxor4d/iw3xo-radiant/workflows/build-debug/develop/Debug%20binaries.zip)&ensp;
[![build-release](https://img.shields.io/github/workflow/status/xoxor4d/iw3xo-radiant/Build-Release/develop?logo=github&label=nightly-release)](https://nightly.link/xoxor4d/iw3xo-radiant/workflows/build-release/develop/Release%20binaries.zip)&ensp;
__<- download__ :: nightly builds - develop branch ( download and install the [latest release](https://github.com/xoxor4d/iw3xo-radiant/releases) before using nightly's )  
<div class="padding-1l"></div>
(_make sure to use the release build and only switch to the debug build if you encounter a crash that you want to report_)
</div>

<br>
&ensp;&ensp; Download the [Latest Release](https://github.com/xoxor4d/iw3xo-radiant/releases) and unzip the contents into your CoD4 root directory.  
&ensp;&ensp; Go into the bin folder and open __`IW3xRadiant.exe`__. 
<p align="right">
	(IW3xRadiant requires the CoD4 Modtools, obviously)<br>
</p>

<div class="padding-1l"></div>
<div align="center" style="margin-top: 2.5rem; margin-bottom: 2.5rem"><div class="seperator-100p"></div></div>
