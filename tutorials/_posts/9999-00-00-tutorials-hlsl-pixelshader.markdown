---
layout:     post
title:      "In-depth :: PixelShaders"
subtitle:   ">> root\\raw\\shader_bin\\shader_src"
date:       2020-01-01 23:54:00
categorie:  Call of Duty 4 - HLSL
permalink: /tutorials/hlsl-pixelshader/
---
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Table of Contents
[Preprocessors](#preprocessors) :: [Constants](#constants) :: [Input-Output](#structs) :: [General Information](#general)
<div class="padding-2l"></div></div> 

<div align="center" markdown="1">
PixelShaders are programmable functions in the rendering pipeline, that get executed for every pixel of a mesh.  
The PixelShader will calculate the color of each pixel, after the model was transformed from 3D model-space to 2D projection-space (screen space) via the VertexShader.
Advanced per-pixel-lighting and diverse texture operations like filters, multi-texturing, bump/normal-mapping or screen-space effects can be implemented using PixelShaders.

<!-- tag for quick links -->
<a name="preprocessors"></a>
<div class="padding-1l"></div>
<div class="seperator-75p"></div>
<div class="padding-1l"></div></div>


# 1. Preprocessors

PixelShaders, just like VertexShaders, need specific preprocessors at the beginning, so that global-shader-constants, defined within __shader_vars.h__, can be mapped correctly.  
For that to work, you obv. have to include __shader_vars.h__ too.

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>/* snippet */</p></div>
{% highlight cpp %}
#define PC
#define IS_VERTEX_SHADER    0
#define IS_PIXEL_SHADER     1 // <
#include <shader_vars.h>
{% endhighlight %}


<!-- tag for quicklinks -->
<a name="constants"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>


# 2. Constants > _root\raw\shader_bin\shader_src\shader_vars.h_

Shader constants, just like Code-Textures or Code-Variables, are exposed by code and pre-defined.  
Most of them are read-only and used to hold general data like:   

<div align="right" markdown="1">
__matrices, time, lighting-information, fog-information, screen-size, parameters assigned within your technique, samplers ...__ 
</div>

<div align="center" markdown="1">
Some constants defined in __shader_vars.h__ can only be used within VertexShaders (constants explicitly registered via __VERTEX_REGISTER__( __index__ )).  
__Note:__ Some of them still work within PixelShaders (eg. _renderTargetSize_). What this should tell you is, that __shader_vars.h__ is not  
a stock file and not 100% correct. Using matrices within PixelShaders will def. throw an error ... trust me, I tried.
</div>


<!-- tag for quicklinks -->
<a name="structs"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>



# 3. Input and Output - structs

The __PixelShader input-struct__ has to include all semantics found in your __VertexShader output-struct__.
So if your VertexShader output-struct was:

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>/* snippet */</p></div>
{% highlight cpp %}
struct VertexOutput
{
    float4 position : POSITION;
    float2 texcoord : TEXCOORD0;
};
{% endhighlight %}

<div class="padding-1l"></div>
Your __PixelShader input-struct__ has to be:

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>/* snippet */</p></div>
{% highlight cpp %}
#include <shader_vars.h>

struct PixelInput   // could be any name really, as we pass our variables using SEMANTICS
{
    float4 position : POSITION;  // same as vertex output
    float2 texcoord : TEXCOORD0; // ^
};
{% endhighlight %}

<div align="center" markdown="1">
<div class="seperator-50p"></div>
<div class="padding-2l"></div>
#### You don't really need a __PixelShader output-struct__, as a PixelShader only outputs a color. See __>>__ [[PixelShader/Output]](#output)  
</div>

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>I'll use one for the sake of this tutorial:</p></div>
{% highlight cpp %}
/* ... */
#include <shader_vars.h>

struct PixelInput 
{
    /* ... */
};

struct PixelOutput  
{
    float4 color    : COLOR;
};
{% endhighlight %}



<div align="center" markdown="1">
<div class="seperator-50p"></div>
<div class="padding-2l"></div>
#### using structs requires your __ps_main function__ to return a completely initialized output struct:  
(this example is assuming that you are using a colorMap assigned to "colorMapSampler")
</div>

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>Example:</p></div>
{% highlight cpp %}
/* ... */
#include <shader_vars.h>

struct PixelInput
{
    float4 position : POSITION;
    float2 texcoord : TEXCOORD0;
};

struct PixelOutput   
{
    float4 color    : COLOR;
};

PixelOutput ps_main( const PixelInput input )  // ps_main returns the output-struct; we also reference our input-struct as "input"
{
    // create the output-struct object
    PixelOutput fragment;  

    float  pulseSpeed = 0.25f;
    float3 textureSample;

    // sample the texture assigned to colorMapSampler using the current uv's
    textureSample = tex2D(colorMapSampler, input.texcoord).rgb;

    // animate the red channel of the sampled texture (pulsing)
    textureSample.r = clamp((textureSample.r * ((gameTime.x * pulseSpeed) + 1.0f / 2.0f)), 0.0f, 1.0f);

    // the returned color has to be a float4
    fragment.color = float4(textureSample, 1.0f);

    // return the struct
    return fragment;
}
{% endhighlight %}

<!-- tag for quick links so we do not show the nav -->
<a name="output"></a>

<div align="center" markdown="1">
<div class="seperator-50p"></div>
<div class="padding-2l"></div>
#### if you do not want to use a struct for the PixelShader output:
</div>

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>Example:</p></div>
{% highlight cpp %}
/* ... */
#include <shader_vars.h>

struct PixelInput
{
    float4 position : POSITION;
    float2 texcoord : TEXCOORD0;
};

float4 ps_main( const PixelInput input ) : COLOR  // ps_main returns a float 4 assigned to the COLOR Semantic
{
    float4 myColor;

    /* color calculations ... */
    
    // simply return a float4 
    return myColor;
}
{% endhighlight %}



<!-- tag for quick links -->
<a name="general"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>



# 4. General information

As I stated before, __always__ make sure that __each and every input__ you defined __contributes to the final color__ that gets output by your shader.  
Microsofts shader compiler tends to optimize your shader and removes everything thats unused, so only only assigning your input to a local variable that is not used for your calculations __is not enough__.

<div class="padding-1l"></div>
<div class="highlight-header"><p>If you don't feel like removing inputs, for testing purposes, heres a small little trick:</p></div>
{% highlight cpp %}
/* ... */
#include <shader_vars.h>

struct PixelInput
{
    float4 position : POSITION;
    float2 texcoord : TEXCOORD0;
    float4 unused   : TEXCOORD1;
};

float4 ps_main( const PixelInput input ) : COLOR  // ps_main returns a float 4 assigned to the COLOR Semantic
{
    float4 myColor;

    /* color calculations not using input.unused ... */
    
    myColor.a = myColor.a + (input.unused.x * 0.00001f); // this wont change a thing but will stop linker from throwing errors :)

    // simply return a float4 
    return myColor;
}
{% endhighlight %}

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links to articles related to PixelShaders
[Techniques](/tutorials/hlsl-techniques#quicklink) :: [VertexShader](/tutorials/hlsl-vertexshader#quicklink)
</div> 