---
layout:     post
title:      "Techniques - In-depth"
subtitle:   ">> root\\raw\\techniques"
date:       2020-01-01 23:57:00
categorie:  Call of Duty 4 - HLSL
permalink: /tutorials/hlsl-techniques/
---
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" markdown="1">
Techniques define shaders, shader-inputs and statemaps that are being used for your current pass. Always make sure that every constant you pass into your shader is actively being used within your shader and referenced by your material template
, otherwise your shader will fail to compile.  
You can mix up Vertex- and PixelShaders as long as the VertexShader ouputs the information that the PixelShader needs. You could also use a stock Vertex- with a custom PixelShader if you so wish, but its somewhat impractical.
Multiple Shader-passes are also supported, but more on that later.

<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l"></div>

Lets have a look at a technique that is using 2 textures (referencing the dynamic material template that was shown here: [Material Templates - In-depth](/tutorials/hlsl-templates/))
</div>

{% highlight cpp %}
{
    stateMap "default2d";                   // defines the statemap to be used >> root\raw\statemaps

    vertexShader 3.0 "hud_myshader"         // custom shader to be used :: shader name (without "vs_3_0_" suffix and extension )
                                            // you only need to append the ".hlsl" extension when you want to use stock shaders 
    {
        // you can pass in constants if you referenced them within your material template like so:
        // distortionScale = material.distortionScale;  
    }

    pixelShader 3.0 "hud_myshader"                  // custom shader to be used :: shader name (without "ps_3_0_" suffix and extension)
                                                    // ^ same applies for pixelshaders
    {
        // ^ same applies for pixelshaders:
        // detailScale = material.detailScale;

        colorMapSampler = material.colorMap;        // pass in the colorMap that was referenced within the material template
        colorMapSampler1 = material.specularMap;    // ^ same for the second "colorMap" that was applied to the specularMap slot
    }

    // variables exposed by the engine
    vertex.position = code.position;                // the current vertex position in model-space 
    vertex.texcoord[0] = code.texcoord[0];          // the UV of the current Vertex
}
{% endhighlight %}

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 1. Samplers

Samplers are defined in __root\raw\shader_bin\shader_src\shader_vars.h__ and either mapped to constant registers or mapped dynamically.  
Each sampler type uses different hard-coded sampler stats that define how it samples the given input image (eg. texture filtering or sampling technique).   
I advice you to use a sampler that fits your input but you can obv. experiment with them if you want. 

<div class="padding-1l"></div>
<div align="right" markdown="1">
##### A list of availible samplers (not sure if every one of them works tho)
</div>

{% highlight cpp %}
sampler     colorMapSampler;
sampler     colorMapSampler1;
sampler     colorMapSampler2;
sampler     colorMapSampler4;

sampler     feedbackSampler;
sampler     colorMapPostSunSampler;

sampler     floatZSampler;
sampler     processedFloatZSampler;
sampler     rawFloatZSampler;

sampler     lightmapSamplerPrimary;
sampler     lightmapSamplerSecondary;

sampler     dynamicShadowSampler;
sampler     shadowCookieSampler;
sampler     shadowmapSamplerSun;
sampler     shadowmapSamplerSpot;
sampler     normalMapSampler;
sampler     normalMapSampler1;
sampler     normalMapSampler2;
sampler     normalMapSampler3;
sampler     normalMapSampler4;
sampler     specularMapSampler;
sampler     specularMapSampler1;
sampler     specularMapSampler2;
sampler     specularMapSampler3;
sampler     specularMapSampler4;
sampler     specularitySampler;
sampler     cinematicYSampler;
sampler     cinematicCrSampler;
sampler     cinematicCbSampler;
sampler     cinematicASampler;
sampler     attenuationSampler;

samplerCUBE skyMapSampler;
samplerCUBE cubeMapSampler;
samplerCUBE reflectionProbeSampler;

sampler     outdoorMapSampler;
sampler     lookupMapSampler; 

sampler     blurSampler;

sampler     detailMapSampler;
sampler     detailMapSampler1;
sampler     detailMapSampler2;
sampler     detailMapSampler3;
sampler     detailMapSampler4;
{% endhighlight %}

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 2. Code-Textures

Code-Textures are exposed by the game but not always valid. They represent the different __Rendertargets__ that the game uses to render   
to "textures" off-screen and are mostly used for post-process effects but also for depth, shadows, lightmaps etc.  
Most of them are only valid when the specific use-case, that they are used for, is active.  
Rendering to code-textures can only be done via engine modifications so these can only be read from.

<div class="padding-1l"></div>
<div align="right" markdown="1">
##### A list of availible Code-Textures
</div>

{% highlight cpp %}
caseTexture
rawFloatZ
processedFloatZ
floatZ
postEffect1
postEffect0
resolvedScene
resolvedPostSun
feedback
dynamicShadow
shadowCookie
shadowmapSpot
shadowmapSun
outdoor
lightmap
identityNormalMap
attenuation
{% endhighlight %}

<div class="padding-1l"></div>

The most useful code-textures are:
{% highlight cpp %}
colorMapPostSunSampler  = sampler.resolvedPostSun;  // framebuffer without hud or lightTweaks but includes the viewmodel
                                                    // can be used for post-processing effects

colorMapSampler         = sampler.floatZ;           // scene depth
{% endhighlight %}

And can be used like:
{% highlight cpp %}
/* ... */

pixelShader 3.0 "hud_myshader"
{
    colorMapPostSunSampler = sampler.resolvedPostSun;   // framebuffer
    colorMapSampler = material.colorMap;                // a second material eg. a noise map 
}

/* ... */
{% endhighlight %}

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 3. Variables

Variables are exposed by the game and hold information about the current vertex that runs through the pipeline.
Variables are always 4D vectors but you can define them as 2D vectors within your shader structs if you only ever need x and y component.
You only define the variables you need and use in your shader or you'll get errors when linking your shader.

<div class="padding-1l"></div>
<div align="right" markdown="1">
##### A list of variables (incomplete)
</div>

{% highlight cpp %}
vertex.position = code.position;                // vertex position in model-space
vertex.normal = code.normal;                    // vertex normal 
vertex.color[0] = code.color;                   // vertex color
vertex.texcoord[0] = code.texcoord[0];          // vertex UV
vertex.texcoord[2] = code.tangent;              // vertex tangent
vertex.texcoord[3] = code.texcoord[1];          // prob. vertex binormal
vertex.texcoord[4] = code.texcoord[2];          // unsure
vertex.texcoord[5] = code.normalTransform[0];   // unsure
vertex.texcoord[6] = code.normalTransform[1];   // unsure
{% endhighlight %}

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links to articles related to Techniques
[Techsets](/tutorials/hlsl-techsets#quicklink) :: [Statemaps](/tutorials/hlsl-statemaps#quicklink) :: [PixelShader](/tutorials/hlsl-pixelshader#quicklink) :: [VertexShader](/tutorials/hlsl-vertexshader#quicklink)
</div> 