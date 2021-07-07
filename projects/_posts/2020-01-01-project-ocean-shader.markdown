---
layout:         post
title:          "Call of Duty 4 :: Ocean Shader"
subtitle:       "realtime / dynamic ocean shader"
description:    "Realtime / dynamic ocean shader, fully customizable in-game via the use of the IW3xo client"
date:           2020-08-22 00:00:00
permalink:      /projects/cod4-ocean/
image:          "/assets/img/shader-ocean/thumb.jpg"
status:         "Done"
---
<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/shader-ocean/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Quick Links
[GitHub Repository](https://github.com/xoxor4d/cod4-shader-ocean) :: [CoD4 Shader Tutorial](https://xoxor4d.github.io/tutorials/hlsl-intro/#compiling) :: [IW3xo](https://github.com/xoxor4d/iw3xo-dev) :: [Discord Server](https://discord.gg/t5jRGbj)
<div class="padding-2l"></div></div> 

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

![](/assets/img/shader-ocean/prev01.jpg# halfsize left) ![](/assets/img/shader-ocean/prev02.jpg# halfsize right) 
![](/assets/img/shader-ocean/prev03.jpg# center)

<div class="padding-1l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

<div markdown="1" style="padding-left: 2rem">
# Overview
   + Shader based on: [https://github.com/tuxalin/water-shader](https://github.com/tuxalin/water-shader)
   + Fully tweakable via in-game GUI or fastfile hotloading (requires IW3xo)
   + Vanilla CoD4 Support
   + Dynamic heightmap generation
   + Displacement
   + Cubemap usage for reflection and radiance
   + Waterdepth dependend refraction and color extiction
   + High wave and shore foam
   + Shore blending
<div class="padding-2l"></div>
# General
   + Supports both xmodels and world geometry while the latter has some visual bugs
   + Supports fullbright and radiants fake-light mode by using a simpler second shader
   + Will only look decent on the first and second day after a dedicated server was started (cod4 gametime bug making it choppy and hella buggy)

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l"></div>

<div class="yt-container">
    <a href="https://www.youtube.com/watch?v=0lDc3uzDOD4">
        <img src="/assets/img/shader-ocean/vid01.jpg" class="yt-image">
        <img src="/assets/img/play_btn.png" class="yt-overlay">
    </a>
</div>

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div class="padding-2l"></div>
# Usage:
<div class="padding-1l"></div>
   1. Clone the repo or download as zip
   2. Copy all files into the cod4 root directory
   3. Open the _shader_ocean.gdt_ in Asset Manager, compile the material and the xmodel
   4. Compile shaders: __worldfx_ocean__ and __worldfx_ocean_unlit__ by either using ShaderGen, included within [cod4-compileToolsXaml](https://xoxor4d.github.io/projects/cod4-compileTools/) or [shader_tool](https://xoxor4d.github.io/tutorials/hlsl-intro/#compiling) directly
   5. Place the __ocean_plane__ xmodel into your map or apply the material to any other kind of xmodel/terrain patch
   6. Tweak in-game using IW3xo (The shader ships with in-game tweaking enabled, requiring IW3xo to be used, see below to disable this if needed)

<div class="padding-2l"></div>
<div class="padding-2l"></div>
# Tweaking in-game using the GUI:
<div class="padding-1l"></div>
   1. Use IW3xo and the built in /devgui command -> ocean tab to tweak the shader however you like. Use the export button to export your settings. 
      - settings will be exported to root/iw3xo/shader_settings/ocean_settings.txt
   2. Overwrite the static shader constants inside the __#else block__ (if USE_CUSTOM_CONSTANTS is not defined) in both the vertex and pixelshader. 
      - Note that both are sharing 3 of the exported constants.
   3. The shader ships with in-game tweaking enabled, requiring IW3xo to be used. 
      - This can be disabled by commenting "//" __#define USE_CUSTOM_CONSTANTS__ in both the vertex and pixelshader.
   4. Disabling __USE_CUSTOM_CONSTANTS__ will enable vanilla cod4 usage. You have to do this before you ship your mod/map.
   5. General shader features such as reflection probe usage or debug ouput can be enabled by defining certain pre-defined preprocessors.
      - eg. #define USE_REFLECTION_PROBES; #define DEBUG_NORMALS etc

<div class="padding-2l"></div>
<div class="padding-2l"></div>
# Tweaking in-game using an addon fastfile:
<div class="padding-1l"></div>
- IW3xo supports loading/reloading of fastfiles and its assets in-game
- Expecting that you already have the shader up and running in your map/mod, do the following:  

<div class="padding-2l"></div>
<div class="highlight-header"><p>​Include the following in your fastfile zone</p></div>
{% highlight cpp %}
material,dynamic_ocean
techset,mc_worldfx_ocean
techset,wc_worldfx_ocean
techset,worldfx_ocean
{% endhighlight %}
<div class="padding-2l"></div>

- Modify the shader however you like and recompile it. Make sure you get no errors when doing so.
- Build the fastfile. Again, watch for errors.
- Load up your map/mod thats including the ocean shader
- Use the following command to load your zone file: __/loadzone your_zone_name__
- The ocean shader should now reflect your changes
- Rinse and repeat

<div class="padding-2l"></div>
<div class="padding-2l"></div>
# Asset Manager Material Settings:
<div class="padding-1l"></div>
1. Template: the material template to be used for this material (deffiles/materials/)
2. String: the techset that will be used for the material. If you created copies of the shader files, you'll need to edit this to reflect your changes
3. colorMap: cubeMap for reflections and sky radiance
  - use IW3xo to generate cubeMaps using the now fixed command __/cubeMapShot 1024 filename__ (dvar r_smp_backend needs to be disabled)
4. normalMap: water normal map
5. specularMap: foam texture (both high wave and shore foam)
6. cosineMap: no longer in use, but could be used within the shader by sampling the alpha channel of the specularMap
</div>