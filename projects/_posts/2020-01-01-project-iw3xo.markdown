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

<div align="center" style="margin-top: -4rem" markdown="1">
#### Quick Links
[GitHub Repository](https://github.com/xoxor4d/iw3xo-dev) :: [Latest Release](https://github.com/xoxor4d/iw3xo-dev/releases) :: [Changelog](https://github.com/xoxor4d/iw3xo-dev/wiki/Changelog) :: [IW3xRadiant](/projects/iw3xo-radiant/)
</div>

<div class="padding-1l"></div>
<h1 align="center">IW3xo - A Call of Duty 4 Client Modification</h1>
<div align="center" style="margin-top: -1.5rem"><div class="seperator-100p"></div></div>
<div class="padding-1l" style="margin-bottom: 0.0rem"></div>

<div align="center" markdown="1">
### IW3xo is a project aimed at developers that includes various modifications and additions.
### You can grab the latest release [here](https://github.com/xoxor4d/iw3xo-dev/releases). The latest changelog can be found [here](https://github.com/xoxor4d/iw3xo-dev/wiki/Changelog).
### Please note that IW3xo is not compatible with CoD4x nor the Steam version of the game.  
<br>
### A quick feature overview can be found below. Go to [In-Depth](#in-depth) for a complete Dvar List and Guids helping you to get where you want.
</div>

<div class="padding-1l"></div>
### [Day-Night cycle](/projects/cod4-daynight/) tweakable via the DevGui
![](/assets/img/iw3xo/gif/feat_daynight.gif)  

<div class="padding-2l"></div>
### [Map exporting](/tutorials/iw3xo-mapexport/) supporting brushes, entities, static models and more
<div class="yt-container">
    <a href="https://www.youtube.com/watch?v=UOjiakKrNdk">
        <img src="/assets/img/iw3xo/feat_mapexport.jpg" class="yt-image">
        <img src="/assets/img/play_btn.png" class="yt-overlay">
    </a>
</div>


<div class="padding-2l"></div>
### Live-link to synchronize selected brushes (with collision), cameras and worldspawn settings between IW3xo and [IW3xRadiant](/projects/iw3xo-radiant/)
<div class="yt-container">
    <a href="https://www.youtube.com/watch?v=SBqZLfCaRdw">
        <img src="/assets/img/iw3xo/gif/feat_livelink.gif" class="yt-image">
        <img src="/assets/img/play_btn.png" class="yt-overlay">
    </a>
</div>

<div class="padding-1l"></div>
### Load SP maps in MP
![](/assets/img/iw3xo/feat_spmap.jpg)  


<div class="padding-1l"></div>
### Debug collision drawing with filtering options
![](/assets/img/iw3xo/collisionDrawType.jpg# left){: style="width: 50%; margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}
![](/assets/img/iw3xo/collisionClip.jpg# right){: style="width: 50%; margin-top: -1rem; margin-left: -1rem; margin-right: -1rem"}


<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>


<div markdown="1" style="padding-left: -2rem">
# Features ([In-Depth](#in-depth))
<div class="padding-2l"></div>
__Memory__
   + Increased Hunk
   + Increased Gmem
   + 3.5GB patch applied to included IW3xo.exe

<br>
<br>
__UI / Gui__
   + Completely new main menu with latest changelog pulled from <https://github.com/xoxor4d/iw3xo-dev/wiki/Changelog>
   + Improved in-game console (eg. drag / resize with the cursor, console output when not using the fullscreen console, ... )
   + Devgui (using ImGui) to access almost all additional dvars eg. map-exporting, movement tweaks / debugging etc ...
   ![](/assets/img/iw3xo/devgui_movement.jpg# right){: style="width: 42%; margin-top: 10rem; margin-right: -1rem"}

<br>
<br>
__File System__
   + Load FastFile addons and IWDs on startup
   + Live FastFile loading/reloading
   + Increased AssetPools
   + Rawfile menu loading / hot-reloading
   + Menu Exporter by [SheepWizard](https://github.com/SheepWizard)
   + Automatically load "reshade.dll" if placed in "iw3xo\bin" 
   + Automatically load "iw3mvm.dll" if placed in "iw3xo\bin" and dvar "load_iw3mvm" is enabled

<br>
<br>
__Map Exporting ([Dvars](#dvars-collision) | [Tutorial](/tutorials/iw3xo-mapexport))__
   + Export brushes, brushmodels, triggers (mapEnts)
   + Option to export merged triangles (quads) as patches
   + Option to export leftover unmerged triangles as patches
   + Option to export entities / reflection probes
   + Option to export static models
   + Option to export a certain section of a map by using a bounding box

<br>
<br>
__Radiant Live-Link (requires [IW3xRadiant](/projects/iw3xo-radiant/))__ 
   + Synchronize up to 16 selected radiant-brushes 
   + Synchronized brushes are colliding (requires a prefab within the map)
   + Synchronized worldspawn settings (sundirection, suncolor, sunlight)
   + Synchronize cameras (radiant \-> server, server \-> radiant or both)

<div class="padding-2l"></div>
Save currently selected brushes using the devgui or console commands
![](/assets/img/iw3xo/gif/feat_livelink_save_selection.gif) 

<br>
<br>
__Rendering__ 
   + Draw debug collision brushes (eg. clip, mantle, multiple, all ...)
   + Filter debug collision by brush indicies, allowing you to display only the collisions you are interested in 
   + Filter debug collisions by distance and material
   + Draw synchronized radiant brushes
   + Trace origin and/or velocity
   + Built-in PostFx shaders like SSAO, Cellshading, Toon ...
   + Direct3D9Ex
   + Borderless fullscreen
   + Custom aspect ratio's
   + Show world and model uv's / texcoords
   + Dump shader binaries at runtime (to iw3xo\shader_dump)
   + Draw xmodel / world surfaces using their wireframe technique
   + Increase rendering buffers such as skinnedCache, smodelCache and various others
   + R_MAX_SKINNED_CACHE_VERTICES and TEMP_SKIN_BUF_SIZE warnings are now dynamic and adjust to their respective buffer sizes
   + Fixed an out of memory error when trying to take screenshots with R_TakeScreenshot when using heavy mods
   + CubeMapShot fixed

<div class="padding-2l"></div>
[Day-Night cycle](/projects/cod4-daynight/) with volumetric clouds tweakable via the DevGui
<div class="yt-container">
    <a href="https://www.youtube.com/watch?v=PlCpgC3jPcM">
        <img src="/assets/img/iw3xo/gif/feat_daynight_clouds.gif" class="yt-image">
        <img src="/assets/img/play_btn.png" class="yt-overlay">
    </a>
</div>

<div class="padding-2l"></div>
Live editing of [Ocean-Shader](/projects/cod4-ocean/) parameters via the DevGui
<div class="yt-container">
    <a href="https://www.youtube.com/watch?v=0lDc3uzDOD4">
        <img src="/assets/img/iw3xo/gif/feat_ocean.gif" class="yt-image">
        <img src="/assets/img/play_btn.png" class="yt-overlay">
    </a>
</div>

<br>
<br>
__Movement__ 
   + Dvar tweakable movement types like quake3/cpm or css/surf
   + Dvar tweakable stock movement settings
   + Dvar tweakable origin and/or velocity tracing
   + Dvar tweakable world axis with fps zones / angles
   + [MDD World Compass](https://github.com/Jelvan1/cgame_proxymod/blob/master/src/compass.c) - Ported by: [n1kjs](https://github.com/Shkerzy)
   + [MDD CampingGaz (cgaz)](https://github.com/Jelvan1/cgame_proxymod/blob/master/src/cg_cgaz.c) - Ported by: [n1kjs](https://github.com/Shkerzy)

<br>
<br>
__Misc__
   + Dvar cheat/write protection removed
   + Added common gsc function like setvelocity(), jumpButtonPressed() ...
   + Fixed mouse lag on some Windows 10 builds (c) [Snake](https://github.com/momo5502)
   + Fixed 500FPS lock on some Windows 10/11 builds

<br>
<br>
![](/assets/img/iw3xo/console01.jpg) 
<br>
<br>

<a name="in-depth"></a>
<div class="padding-2l"></div>
<div markdown="1" style="padding-left: 2rem">
# In-Depth Features / Functions / Dvars

<div class="padding-2l"></div>
<a name="dvars-devgui"></a>
<div class="highlight-header"><p>DevGui</p></div>
{% highlight cpp %}
[Hotkeys]
|-> Home       :: Opens ImGui Demo menu (DEBUG Build only)
|-> End        :: Opens DevGui (DEBUG Build only)

[Commands]
|-> devgui        :: opens the devgui
|-> devgui_demo   :: opens the ImGui demo menu
{% endhighlight %}


<div class="padding-2l"></div>
<div class="highlight-header"><p>In-Game Console</p></div>
{% highlight cpp %}
[Hotkeys]
|-> F1         :: Enable mouse cursor (in-game)
|-> F2         :: Reset Console
|-> Mouse 1    :: Press and hold inputbar to move the console. Press and hold the resize-arrow to resize the console (bottom right)

[Dvars]
|-> xo_con_outputHeight          :: line amount for mini-con output window
|-> xo_con_maxMatches            :: maximum amount of matches to draw
|-> xo_con_padding               :: padding from window borders (default console state (F2))
|-> xo_con_useDepth              :: use depth-preview shader as background for output window
|-> xo_con_hintBoxTxtColor ...   :: change console text colors
|-> xo_con ...
|-> con_minicon_position         :: change position of the minicon
|-> con_minicon ...
{% endhighlight %}


<div class="padding-2l"></div>
<div class="highlight-header"><p>Custom Shaders</p></div>
{% highlight cpp %}
[Types]
|-> XO_SHADEROVERLAY 1      :: SSAO (dvars : xo_ssao_)
|-> XO_SHADEROVERLAY 2      :: CELLSHADING
|-> XO_SHADEROVERLAY 3      :: OUTLINER (dvars : xo_outliner_)
|-> XO_SHADEROVERLAY 4      :: FULLSCREEN-DEPTH
|-> XO_SHADEROVERLAY 5      :: CUSTOM (dvar : xo_shaderoverlay_custom)

[Dvars]
|-> xo_shaderoverlay_custom :: material to be used as a full screen overlay shader
|-> xo_shaderdbg_matrix     :: debug transformation matrices
{% endhighlight %}


<div class="padding-2l"></div>
<div class="highlight-header"><p>Movement</p></div>
{% highlight cpp %}
[Preset Commands]
|-> pm_preset_cs
|-> pm_preset_q3
|-> pm_preset_stock

[Dvars]
|-> mdd_cgaz                     :: display mDd CampingGaz HUD
|-> mdd_cgaz_ground              :: show true ground zones
|-> mdd_cgaz_min_speed           :: speed at which to draw cgaz
|-> mdd_cgaz_yh                  :: cgaz y position and thickness
|-> mdd_cgaz_rgbaNoAccel         :: color of no accel zones
|-> mdd_cgaz_rgbaPartialAccel    :: color of partial accel zones
|-> mdd_cgaz_rgbaFullAccel       :: color of full accel zones
|-> mdd_cgaz_rgbaTurnZone        :: color of turn zones

|-> mdd_compass                  :: display mDd world compass
|-> mdd_compass_yh               :: compass y position and thickness
|-> mdd_compass_quadrant_rgbas0  :: color 0 to 90 quadrant
|-> mdd_compass_quadrant_rgbas1  :: color 90 to 180 quadrant
|-> mdd_compass_quadrant_rgbas2  :: color 180 to 270 quadrant
|-> mdd_compass_quadrant_rgbas3  :: color 270 to 360 quadrant
|-> mdd_compass_ticks_rgba       :: color of ticks

|-> pm_debug_drawAxis            :: draw axial information (axis/fps Zones)
|-> pm_debug_drawAxis_radius     :: radius of axis/zones circle
|-> pm_debug_drawAxis_height     :: height offset (from player origin)
|-> pm_debug_drawAxis_col ...    :: color of zone/s
|-> pm_debug_traceOrigin         :: trace player origin (multiple options)
|-> pm_debug_traceVelocity       :: trace player velocity (multiple options)

|-> pm_hud_enable                :: disable debug hud with speed/movementtype display
|-> pm_movementType              :: movement TYPES
|-> pm_cpm_ ....                 :: q3 settings
|-> pm_cs_ ....                  :: cs settings
|-> pm_ ......
{% endhighlight %}


<div class="padding-2l"></div>
<a name="dvars-collision"></a>
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
<a name="dvars-mapexport"></a>
<div class="highlight-header"><p markdown="1">Debug Collision Brushes - Map Exporting :: [[Tutorial]](/tutorials/iw3xo-mapexport)</p></div>
{% highlight cpp %}
[Commands]
|-> mapexport                   :: export highlighted brushes + options or bounding box selection
|-> mapexport_selectionAdd      :: adds a point to the bounding box (needs mapexport_selectionMode and 2 points in total)
|-> mapexport_selectionClear    :: reset the bounding box (needs mapexport_selectionMode)

[Dvars]
|-> mapexport_selectionMode     :: export only certain parts of a map by using a bounding box (see commands above)
|-> mapexport_brush5Sides       :: export brushes that only consist of 5 sides
|-> mapexport_brushEpsilon1     :: brushside generation epsilon 1 (adv. only)
|-> mapexport_brushEpsilon2     :: brushside generation epsilon 2 (adv. only)
|-> mapexport_brushMinSize      :: only export brushes (with more then 6 sides) if their diagonal length is greater then this
|-> mapexport_writeQuads        :: export merged triangles as quads, if enabled
|-> mapexport_writeTriangles    :: export leftover triangles, if enabled
|-> mapexport_writeEntities     :: export map entities, if enabled
|-> mapexport_writeModels       :: export static models, if enabled
{% endhighlight %}


<div class="padding-2l"></div>
<div class="highlight-header"><p>Radiant Live-Link</p></div>
{% highlight cpp %}
[Commands]
|-> radiant_saveSelection       :: save the current brush selection
|-> radiant_clearSaved          :: clear saved brushes

[Dvars]
|-> radiant_live                :: enables live-Link
|-> radiant_liveDebug           :: enables live-Link debug prints
|-> radiant_livePort            :: port used for live-Link (has to match radiant)
|-> radiant_syncCamera          :: camera sync modes (radiant->game, game->radiant, both)
|-> radiant_brushColor          :: color of debug brushes created with radiant
|-> radiant_brushCollision      :: enable brush collision (map needs to include prefab <dynamic_collision_bmodels.map>)
|-> radiant_brushLit            :: enable custom-shader usage (unlit fake-lighting)
|-> radiant_brushWireframe      :: enable additional wireframe
|-> radiant_brushWireframeColor :: color of wireframe
{% endhighlight %}


<div class="padding-2l"></div>
<div class="highlight-header"><p>Menus</p></div>
{% highlight cpp %}
[Commands]
|-> menu_loadlist_raw <menulist_name.txt>                :: rawfile load/reload menus defined in a menulist. 
                                                            files need to be in devraw directories (needs fs_usedevdir)   
|-> menu_list                                            :: prints a list of all loaded menus to the console
|-> menu_open <menu_name>                                :: opens a loaded menu by name
|-> menu_open_ingame <menu_name>                         :: opens a loaded menu by name (ingame)
|-> menu_closebyname <menu_name>                         :: close a loaded and visible menu by name
|-> menu_export <menu_name> <[optional] subdir>          :: exports the specified menu
|-> menu_export_itemdefs <menu_name> <[optional] subdir> :: exports all itemdefs of the specified menu
{% endhighlight %}


<div class="padding-2l"></div>
<div class="highlight-header"><p>Renderer</p></div>
{% highlight cpp %}
[Dvars]
|-> r_noborder                  :: borderless fullscreen (needs vid_xpos/ypos 0)
|-> r_d3d9ex                    :: enables extended dx9 interface (on by default)
|-> r_aspectRatio               :: use 4 / custom to enable custom aspect ratios (r_aspectRatio_custom)
|-> r_aspectRatio_custom        :: 21:9 = 2.333 / 32:9 = 3.5555
|-> r_dumpShaders               :: Dump visible shaders at runtime (iw3xo/shader_dump)
|-> r_wireframe_world           :: Draw world objects using their wireframe technique
|-> r_wireframe_xmodels         :: Draw xmodels using their wireframe technique
|-> r_debugShaderTexcoord       :: Show surface UVs / Texcoords
|-> r_dayAndNight               :: Enable day and night cycle
|-> r_fogTweaks                 :: Enable framefog tweaks
|-> r_fogTweaksColor            :: Framefog color
|-> r_fogTweaksStart            :: Framefog start
|-> r_fogTweaksDensity          :: Framefog density

// DISABLE r_fastSkin if you are changing these dvars or the client will crash when hitting the old limit
|-> r_buf_skinnedCacheVb        :: Size of skinnedCache Vertexbuffer (Size * 2 will be allocated) in Megabytes
|-> r_buf_smodelCacheVb         :: Size of smodelCache Vertexbuffer in Megabytes
|-> r_buf_smodelCacheIb         :: Size of smodelCache Indexbuffer in Megabytes
|-> r_buf_tempSkin              :: Size of tempSkin buffer in Megabytes
|-> r_buf_dynamicVertexBuffer   :: Size of dynamic Vertexbuffer in Megabytes
|-> r_buf_dynamicIndexBuffer    :: Size of dynamic Indexbuffer in Megabytes
|-> r_buf_preTessIndexBuffer    :: Size of preTess Indexbuffer (Size * 2 will be allocated) in Megabytes

[Commands]
|-> cubeMapShot                 :: fully works now -> disable r_smp_backend when using it
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Misc</p></div>
{% highlight cpp %}
[Commands]
|-> help                   :: link, opens IW3xo Project page
|-> iw3xo_github           :: link, opens IW3xo Github repo
|-> iw3xo_radiant_github   :: link, opens IW3xRadiant Github repo
|-> loadzone <zoneName>    :: load/reload zones (fastfiles)
{% endhighlight %}


<div class="padding-2l"></div>
<div class="highlight-header"><p>SP map loading</p></div>
{% highlight cpp %}
- load spmod
- change gametype to "dm"
- "devmap coup" (or any other sp map)
{% endhighlight %}

<div align="center" style="margin-top: 6rem; margin-bottom: -2rem" markdown="1">
None of this would be possible without the friends over at [XLabs](https://github.com/XLabsProject) and [Plutonium](https://plutonium.pw/)  
Much love ❤ 
</div> 