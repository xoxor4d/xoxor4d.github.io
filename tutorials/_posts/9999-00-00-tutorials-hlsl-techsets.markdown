---
layout:     post
title:      "In-depth :: Techsets"
subtitle:   ">> root\\raw\\techsets"
date:       2020-01-01 23:58:00
categorie:  hlsl
permalink: /tutorials/hlsl-techsets/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/compileTools/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Table of Contents
[Techset-Suffix](#suffix) :: [ShaderModel 2](#sm2) :: [Assign Techniques](#techniques) :: [Additional Info](#info)
<div class="padding-2l"></div></div> 

<div align="center" markdown="1">
Techsets are rather simple and there is not much to know about them really. They just define different techniques for different lighting/rendering states within the game.
There is one thing thats kinda tricky tho, ... knowing what states are needed and what they are needed for.



<!-- tag for quick links -->
<a name="suffix"></a>
<div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 1. Techset Suffixes

Different suffixes and multiple techsets might be needed, depending on where you use your material.  

{% highlight cpp %}
["2D-Materials"] :: requires 1 techset without any suffix at all
                    (eg. my_techset.techset)

["3D-Materials"] :: requires atleast 2 techsets, one without any suffix just like "2D" only ones and:
        > Models :: needs an additional "mc_" suffixed one (eg. mc_my_techset.techset)
      > Geometry :: needs an additional "wc_" suffixed one (eg. wc_my_techset.techset)
  > Models & Geo :: needs both of the above (eg. mc_my_techset.techset & wc_my_techset.techset)
{% endhighlight %}



<!-- tag for quick links -->
<a name="sm2"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 2. Techsets for ShaderModel 2

Like stated in the introduction: Techsets in __root\raw\techsets__ will be used by GPUs running _ShaderModel 3_, but CoD4 also supports _ShaderModel 2_ 
so you have to create copies of your techsets and place them into __​root\raw\techsets\sm2__ (otherwise get'll errors when linking your fastfile).  
These will obv. not work on SM2 hardware but I personally do not care about that.




<!-- tag for quick links -->
<a name="techniques"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 3. Assigning Techniques

Only a single technique can be assigned to a state but multiple states can be assigned to a single technique.  
Not defining a state used by the game results in .. ? (unsure)

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>2D only techsets</p></div>
{% highlight cpp %}
"unlit":
    my_hud_technique_name;
{% endhighlight %}

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>"Model techsets with prefix "mc_"</p></div>
{% highlight cpp %}
/* eg. viewmodels */
/* most techniques used for models have a _dtex suffix*/

"fakelight normal":
    fakelight_normal_dtex;

"fakelight view":
    fakelight_view_dtex;

"case texture":
    case_texture_dtex;

"shaded wireframe":             
    wireframe_shaded_dtex;

"solid wireframe":
    wireframe_solid_dtex;

"depth prepass":
    zprepass;

"build shadowmap depth":
    build_shadowmap_model;

"build shadowmap color":
    build_shadowmap_color_dtex_sm2;

"build floatz":
    build_floatz_dtex;

"unlit":                    // assigning multiple states to a single technique:
"lit":
"lit sun":
"lit sun shadow":
"lit spot":
"lit spot shadow":
"lit omni":
"lit omni shadow":
"light omni":
"light spot":
"light spot shadow":
    my_model_technique_name;    // the only thing you need to change for viewmodels really
                                // but you have to turn off dynamic lights in-game or your viewmodel start flickering when ads'ing :p
"sunlight preview":
    sunpre_r0c0_dtex;

"shadowcookie caster":
    shadowcookie_caster_dtex;

"shadowcookie receiver":
    shadowcookie_receiver_dtex;

{% endhighlight %}

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>World techsets with suffix "wc_"</p></div>
{% highlight cpp %}
/* example for world geometry*/

"fakelight normal":
"fakelight view":
    vertcol_simple;

"case texture":
    case_texture;

"shaded wireframe":
    wireframe_shaded;

"solid wireframe":
    wireframe_solid;

"depth prepass":
    zprepass;

"build floatz":
    build_floatz;

"unlit":
    my_fullbright_technique_name;   // if you would like to use a different technique that calls different shaders
                                    // when using r_fullbright for example
"lit":
"lit sun":
"lit sun shadow":
"lit spot":
"lit spot shadow":
"lit omni":
"lit omni shadow":
    
    my_technique_name;
{% endhighlight %}

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>Sky techsets with suffix "wc_"</p></div>
{% highlight cpp %}
/* example for skies*/

"shaded wireframe":
    wireframe_shaded;

"solid wireframe":
    wireframe_solid;

"fakelight normal":         // radiant doesn't like heavy shaders so if you get errors within radiant
"fakelight view":           // assign a technique with simpler shaders to these 2 here
"unlit":
"lit":
"lit sun":
"lit sun shadow":
"lit spot":
"lit spot shadow":
"lit omni":
"lit omni shadow":

"lit instanced":
"lit instanced sun":
"lit instanced sun shadow":
"lit instanced spot":
"lit instanced spot shadow":
"lit instanced omni":
"lit instanced omni shadow":
    
    my_sky_technique;
{% endhighlight %}


<!-- tag for quick links -->
<a name="info"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 4. Additional Information / Engine Background (SM / HSM)

<div class="highlight-header"><p>Techset abbreviations</p></div>
{% highlight cpp %}
w       // world
wc      // world color
m       // model
mc      // model color
l       // light
sm      // shadow
hsm     // hardware shadow
scroll  // scrolling texcoords
r0      // reflection sample
c0      // colormap
d0      // detailmap
n0      // normalmap
s0      // specularmap
{% endhighlight %}

Using the __l_sm__ prefix for techsets allows the engine to remap it to a __l_hsm__ (hardware shadowmapping) techset if cod4 detects that your GPU supports HSM. 
This means that you need to have the same techset name but prefixed with __l_hsm__. Linker will throw an error if you don't.

Example: most, if not all cod4 weapons use the __l_sm_r0c0s0__ techset. If your GPU supports HSM, the engine will now look for the __l_hsm__ prefixed techset. Since this example is about models, the engine will look for the __mc__ prefix. That means that the actual techset being used is __mc_l_hsm_r0c0s0__.  

<div align="center" markdown="1">
Confused? This might clear things up for you: [cod4-shader-reversed-weapon](https://github.com/xoxor4d/cod4-shader-reversed-weapon)
</div>



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


<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links to articles related to Techsets
[MaterialTemplates](/tutorials/hlsl-templates#quicklink) :: [Techniques](/tutorials/hlsl-techniques#quicklink)
</div> 

