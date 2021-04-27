---
layout:         post
title:          "Call of Duty 4 :: Stock Weapon Shaders"
subtitle:       "Partially reversed cod4 weapon shaders"
description:    "Partially reversed cod4 weapon shaders including the most common lighting states as a base for custom weapon effects"
date:           2021-04-25 00:00:00
permalink:      /projects/cod4-reversed-weapon-shaders/
image:          "/assets/img/shader-weapon/thumb.jpg"
status:         "WIP - PUBLIC"
---
<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/shader-weapon/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Quick Links
[GitHub Repository](https://github.com/xoxor4d/cod4-shader-reversed-weapon) :: [CoD4 Shader Tutorial](https://xoxor4d.github.io/tutorials/hlsl-intro/#compiling) :: [Discord Server](https://discord.gg/t5jRGbj)
<div class="padding-2l"></div></div> 

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: 0.5rem"></div>

![](/assets/img/shader-weapon/deagle.jpg# center)

<div class="padding-1l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: 0.5rem"></div>


<div markdown="1" style="padding-left: 2rem; padding-right: 2rem">
<div class="highlight-header"><p>Includes Techniques/Shaders for the following lighting states</p></div>
{% highlight cpp %}
unlit  
lit  
lit sun  
lit sun shadow  
lit spot  
lit spot shadow  
light omni
{% endhighlight %}
<div class="padding-2l"></div>

It is worth noting that techniques using shadow-mapping require HSM (hardware shadow-mapping) to be supported by the GPU. The GPU also needs to support ShaderModel 3 + the client needs to use it aswell (r_rendererPreference / r_rendererInUse). 

If one of the above requirements isn't fulfilled or you find yourself in a lighting situation thats not covered by this repo, stock cod4 techniques / shaders will be used (non-hsm variants, stock hsm variants or stock ShaderModel 2 techsets located in `techsets/sm2`).
<div class="padding-2l"></div>

# Engine Background (SM / HSM)
Most, if not all cod4 weapons use the __l_sm_r0c0s0__ techset (-light, -shadowmap, -reflection-color-specular ). If cod4 detects that your GPU supports HSM, the engine will remap __l_sm__ to __l_hsm__. Since this repo is about models (weapon models in particular) the engine will also add the __mc__ prefix. That means that the main techset for all techniques is __mc_l_hsm_r0c0s0__. 

Because I don't want to modify stock techsets, techniques and shaders, I've changed __r0c0s0__ to __xo_rcs__ (note: both are 6 chars long giving you the ability to replace __l_sm_r0c0s0__ with __l_sm_xo_rcs__ in all kinds of materials using the __l_sm_r0c0s0__ techset).
<div class="padding-2l"></div>

# Compiling
[Grab and drop](https://github.com/xoxor4d/cod4-shader-reversed-weapon) files into __cod4/raw/__ and compile shaders with [cod4-compileTools](/projects/cod4-compileTools/) or refer to the following tutorial section [hlsl-intro/#compiling](/tutorials/hlsl-intro/#compiling).

Please note that you need the __shader_vars.h__ header file in __shader_bin/shader_src__ that comes with my compileTools or the shader package
<a href="https://drive.google.com/open?id=14xNhEJtRVFaYG3rQZOV7fvjmd2R7CwUP">v1.1_hlsl_xoxor4d.zip</a> and is therefore not included here.
<div class="padding-2l"></div>

# Modifications / Additions
If you want to change the used techniques or replace stock ones, you only need to do so in __mc_l_hsm_xo_rcs.techset__.  
If you want to add "effects" to your gun, you'll need to add that effect to each and every technique / shader so its consistent accross different lighting states. You could also use different effects for different lighting states if you wish.  

I've included a Visual Studio solution as I like using Tim G. Jones <a href="https://marketplace.visualstudio.com/items?itemName=TimGJones.HLSLToolsforVisualStudio">HLSL Tools for Visual Studio</a>
<div class="padding-2l"></div>

<div class="highlight-header"><p>Techset Lighting States Explained</p></div>
{% highlight cpp %}
"fakelight normal"              // radiant fakelight
"fakelight view":               // radiant fakelight
"case texture":                 // radiant only  
"shaded wireframe":             // radiant only  
"solid wireframe":              // radiant only  
"debug bumpmap":                // r_debugShader 1-4  
"debug bumpmap instanced":      // ^ grouped objects like grass
"depth prepass":                
"build shadowmap depth":  
"build shadowmap color":  
"build floatz":  
"unlit":                        // fullbright  
"lit":                          // sm_enable 0 + not in sun || sm_enable 1 + not in sun  
"lit sun":                      // sm_enable 0 + in sun  
"lit sun shadow":               // sm_enable 1 + in sun  
"lit spot":                     // sm_enable 0 :: spotlight / dlight  
"lit spot shadow":              // sm_enable 1 :: spotlight / dlight  
"lit omni":                     // no clue  
"lit omni shadow":              // no clue  
"lit instanced":                // prob. grouped objects like grass / trees
"lit instanced sun":            // ^
"lit instanced sun shadow":     // ^
"lit instanced spot":           // ^
"lit instanced spot shadow":    // ^
"lit instanced omni":           // ^
"lit instanced omni shadow":    // ^
"light omni":                   // fx omni lights  
"light spot":                   // fx spot lights  
"light spot shadow":            // fx shadow-casting spot lights  
"sunlight preview":             // radiant only?  
"shadowcookie caster":          // shadow caster
"shadowcookie receiver":        // shadow receiver
{% endhighlight %}

</div>