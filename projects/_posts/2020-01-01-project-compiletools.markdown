---
layout:         post
title:          "Call of Duty 4 :: Compile Tools"
subtitle:       "extending the features of the stock CoD4-compileTools"
description:    "Extending the features of the stock CoD4-compileTools. Modern UI with a build-in console and highlighting. A Shader-generator and GLSL->HLSL syntax converter."
date:           2020-04-03 00:00:00
permalink:      /projects/cod4-compileTools/
image:          "/assets/img/compileTools/thumb.jpg"
status:         "Done"
---
<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/compileTools/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Quick Links
[GitHub Repository](https://github.com/xoxor4d/cod4-compileToolsXaml) :: [Latest Release](https://github.com/xoxor4d/cod4-compileToolsXaml/releases)
<div class="padding-2l"></div></div> 

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

![](/assets/img/compileTools/prev01.jpg# halfsize left) ![](/assets/img/compileTools/prev02.jpg# halfsize right) 

<div class="padding-1l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

<div markdown="1" style="padding-left: 2rem">
# Features
<div class="padding-2l"></div>
__Interface__
   + New UI using xaml
   + Changeable icons
   + Built-in console with text highlighting
<div class="padding-2l"></div>
__General Features__
   + Individual commandline-settings for bsp / light / run
   + Build/copy all custom images used within the map to the maps-iwd
   + Option to copy Fastfiles to "root\usermaps\mapname\\" after building them
   + Option to change mp/radiant executable names
<div class="padding-2l"></div>
__Shader Generator__
   + Automatically generate shaders by using templates found in: "\bin\CoD4CompileTools\ShaderGen\\"
   + Includes pre-built templates for: 2D, sky, viewmodel, xmodel and world materials, each with multiple options to choose from
   + Option to "inject" shaders/techsets into stock weapon viewmodels (custom public models etc ..)
   + Option to compile shaders after generation
   + A list of all existing shaders in "shader_bin\shader_src\\" with options to quickly compile or edit them
   + Quicklinks to all shader related folders
   + A simple GLSL -> HLSL syntax converter
</div>

<div class="padding-1l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: 1.5rem"></div>

![](/assets/img/compileTools/prev03.jpg# centered) 