---
layout:     post
title:      "In-depth :: Material Templates"
subtitle:   ">> root\\deffiles\\materials"
date:       2020-01-01 23:58:00
categorie:  Call of Duty 4 - HLSL
permalink: /tutorials/hlsl-templates/
---
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" markdown="1">
Material templates define inputs, constants, textures, shader states and the techniques that are being used by your materials. Material templates are quite dynamic and can be written in such a way that they are able to support multiple different but similar shaders. That means that you do not have to create a seperate template for each new shader you write if you have a well written template.
</div>

<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
Remember that scrolling hud element shader we created within the introduction? The template we used was very basic and only supports 1 texture and uses a hard-coded techset. What if we want to use a second texture within a shader?
</div>

<div class="padding-1l"></div>
<div class="highlight-header"><p>Example of a more dynamic template that can use 2 different techsets depending on your material settings in AssetManager:</p></div>
{% highlight cpp %}
#define HUD_SHADER_SUFFIX   "2d_scroll_c0"      // techset suffix for materials using this template

#define USE_SECOND_TEX      0                   // default value if we only use a single colorMap
#define SECOND_TEX_PREFIX   "c1"                // the prefix we will add to our techset if using a second colorMap

// ---------------------
// check our current material

#if "$specColorMap$" != ""              // check if the material uses a "specular map"
    #define USE_SECOND_TEX 1            // set our "bool" to true if the material is using a second texture

// ---------------------
// set the techset used by the material

#if USE_SECOND_TEX
    techniqueSet( HUD_SHADER_SUFFIX + SECOND_TEX_PREFIX );      // using a second texture so use techset "2d_scroll_c0c1"
#else
    techniqueSet( HUD_SHADER_SUFFIX );                          // otherwise use "2d_scroll_c0"
#endif

// ---------------------
// setup textures

#if "$colorMap$" == ""                                      // check if the "colorMap" field in Asset Manager is empty
    #error "missing specularMap! ( missing color map! )"    // throw an error if it is

#else
    // define the colorMap and assign related values set from within Asset Manager (@field_in_asset_manager@)
    "colorMap" = streamable map( "@tileColor@", "@filterColor@", "$colorMap$", @nopicmipColor@ ) "@formatColor@" : "colorMap";
#endif

#if USE_SECOND_TEX
    // we are going to use the specular map field as a second colorMap
    "specularMap" = streamable map( "@tileColor@", "@filterColor@", "$specColorMap$", @nopicmipColor@ ) "@formatColor@" : "specularMap";
#endif

// ---------------------

// not really sure why we only reference the colorMap field here, but thats how its done
refImage( "$colorMap$" );
{% endhighlight %}

<div class="padding-1l"></div>

<div align="center" markdown="1">
The template will choose a fitting techset for your material settings set within Asset Manager.  
Materials using only a single colorMap will be using the techset __2d_scroll_c0__  while materials that use a second texture will use __2d_scroll_c0c1__.  
You obv. have to create 2 techsets now, each calling their own technique and each technique its own shaders.
</div>



<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l"></div>

<div class="highlight-header"><p>Including other templates</p></div>
{% highlight cpp %}
#include "my_other_template.template"
{% endhighlight %}

<div class="highlight-header"><p>Using the custom-string field below the template field</p></div>
{% highlight cpp %}
#if "@customString@" != ""
    #define MY_PREFIX "@customString@"
#else
    #define MY_PREFIX ""
#endif

techniqueSet( "my_shader_desc_" + MY_PREFIX );
{% endhighlight %}

<div class="highlight-header"><p>Using constants</p></div>
{% highlight cpp %}
constantTable
{
    // constants can be used for anything within the shader if you want some more customization options without modifying the shader itself
    // you obv. have to pass them into your shader via your technique

    "colorTint" = float4( @,colorTint@ );
    "distortionScale" = float4( @distortionScaleX@, @distortionScaleY@, 0, 0 );

    /*. . .*/
}
{% endhighlight %}

<div class="highlight-header"><p>Not using any texture at all</p></div>
{% highlight cpp %}
// you shader might not need any textures at all but you still need to reference an image
// now your template could look as simple as:

#include "commonsetup.template"

techniqueSet( "my_techset" );

refImage( "$white" );   // using a default texture
{% endhighlight %}

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links to articles related to material templates
[Introduction](/tutorials/hlsl-intro#quicklink) :: [Techsets](/tutorials/hlsl-techsets#quicklink)
</div> 