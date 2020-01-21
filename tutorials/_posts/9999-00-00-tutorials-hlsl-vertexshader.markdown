---
layout:     post
title:      "In-depth :: VertexShaders"
subtitle:   ">> root\\raw\\shader_bin\\shader_src"
date:       2020-01-01 23:55:00
categorie:  Call of Duty 4 - HLSL
permalink: /tutorials/hlsl-vertexshader/
---
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Table of Contents
[Preprocessors](#preprocessors) :: [Constants](#constants) :: [Input-Output](#structs)
<div class="padding-2l"></div></div> 

<div align="center" markdown="1">
VertexShaders are programmable functions in the rendering pipeline, that get executed for every vertex of a mesh.  
They are used to transform the individual attributes of vertices, eg. __vertex colors, normals, position, rotation, scale, lighting__ and most importantly,  
__transformations__ from one space (dimension) into another (eg. __model-space to projection-space__).



<!-- tag for quick links -->
<a name="preprocessors"></a>
<div class="padding-1l"></div>
<div class="seperator-75p"></div>
<div class="padding-1l"></div>
</div>

# 1. Preprocessors

VertexShaders need specific preprocessors at the beginning, so that global-shader-constants, defined within __shader_vars.h__, can be mapped correctly.  
For that to work, you obv. have to include __shader_vars.h__ too.

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>/* snippet */</p></div>
{% highlight cpp %}
#define PC
#define IS_VERTEX_SHADER    1 // <
#define IS_PIXEL_SHADER     0
#include <shader_vars.h>
{% endhighlight %}



<!-- tag for quick links -->
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




<!-- tag for quick links -->
<a name="structs"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 3. Input and Output - structs

The vertex input-struct has to include all semantics that are defined within the technique that called your shader. See __>>__ [[Technique/Semantics]](/tutorials/hlsl-techniques#semantics)  
Using structs to manage your In- and Output is advised, tho there are different ways of managing your data.  

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>/* snippet */</p></div>
{% highlight cpp %}
#include <shader_vars.h>

struct VertexInput  // struct that holds the input data declared within a technique
{
    float4 position : POSITION;     // declare Semantic "POSITION" as position (vertex position)
    float4 normal   : NORMAL;       // ^ (vertex normal)
    float4 color    : COLOR;        // ^ (vertex color)
    float2 texcoord : TEXCOORD0;    // ^ (vertex UV as float2 because we only need the x and y)
};

struct VertexOutput // vertex shader output data (used as input for the pixel shader)
{
    float4 position : POSITION;     // the transformed vertex position (not usable in the pixel shader)
    float4 normal   : NORMAL;       // eg. we want to use vertex normal within the pixelshader
    float4 color    : COLOR;        // ^
    float2 texcoord : TEXCOORD0;    // ^
};
{% endhighlight %}

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div align="center" markdown="1">
#### the above is an example, using a technique with the following semantics defined:
</div>

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>/* snippet */</p></div>
{% highlight cpp %}
vertex.position     = code.position;    // vertex position in model-space
vertex.normal       = code.normal;      // vertex normal 
vertex.color[0]     = code.color;       // vertex color
vertex.texcoord[0]  = code.texcoord[0]; // vertex uv
{% endhighlight %}


<div align="center" markdown="1">
<div class="seperator-50p"></div>
<div class="padding-2l"></div>
#### using structs requires your __vs_main function__ to return a completely initialized output struct:
</div>

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>Example:</p></div>
{% highlight cpp %}
/* ... */
#include <shader_vars.h>

struct VertexInput
{
    float4 position : POSITION;
    float4 normal   : NORMAL;
    float4 color    : COLOR;
    float2 texcoord : TEXCOORD0;
};

struct VertexOutput
{
    float4 position : POSITION;
    float4 color    : COLOR;
    float4 normal   : NORMAL;
    float2 texcoord : TEXCOORD0;
};

VertexOutput vs_main( const VertexInput input )  // vs_main returns the output-struct; we also reference our input-struct as "input"
{
    // create the output-struct object
    VertexOutput output;   

    // transform the vertex from model to projection-space and put the result into the output-struct member "position"
    output.position = mul(float4(input.position.xyz, 1.0f), worldViewProjectionMatrix); 
	
    // we need to pass input parameters into the pixelshader if they werent used for any calculations for other ouput-struct members
    output.color = input.color;
    output.normal = input.normal;
    output.texcoord = input.texcoord;

    // return the fully initialized struct
    return pixel;
}
{% endhighlight %}


<div align="center" markdown="1">
<div class="seperator-50p"></div>
<div class="padding-2l"></div>
#### if you only need some of the input parameters within the VertexShader, eg. to modify vertex positions, you don't need to pass them to your PixelShader:
</div>

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>Example:</p></div>
{% highlight cpp %}
/* ... */

struct VertexOutput
{
    float4 position : POSITION; 
    //float4 color    : COLOR;  // we only use color inside the vertex shader to modify vertex positions
    float4 normal   : NORMAL;       
    float2 texcoord : TEXCOORD0;
};

VertexOutput vs_main( const VertexInput input ) 
{
    VertexOutput output;   

    float waveStrength = 20.0f;
    
    // animate the vertex z-coord by its alpha channel value (xmodels that use vertex-colors like flags or moving grass) 
    float modZ = input.position.z + (input.color.a * (sin(gameTime.w) * waveStrength));
    
    // transform the vertex with its stock xy-coords and modified z-coord
    output.position = mul(float4(input.position.xy, modZ, 1.0f), worldViewProjectionMatrix); 
	
    //output.color = input.color; // we no longer pass color as we only needed it inside the vertex shader
    output.normal = input.normal;
    output.texcoord = input.texcoord;

    // return the fully initialized struct
    return pixel;
}
{% endhighlight %}


<div align="center" markdown="1">
<div class="seperator-50p"></div>
<div class="padding-2l"></div>
#### You can use the TEXCOORD 0-6 Semantic if you want to use certain values or constants within your PixelShader,  
that are only accessible within the VertexShader stage:
</div>

<div class="padding-1l" style="margin-bottom: 0.5rem"></div>
<div class="highlight-header"><p>Example:</p></div>
{% highlight cpp %}
struct VertexInput
{
    float4 position : POSITION;     // vertex position
    float2 texcoord : TEXCOORD0;    // vertex uv
};

struct VertexOutput
{
    float4 position : POSITION;     // transformed vertex position
    float2 texcoord : TEXCOORD0;    // vertex uv
    float4 worldPos : TEXCOORD1;    // pass the untransformed vertex position inside TEXCOORD1
    float4 eyePos   : TEXCOORD2;    // pass the eyePos
};

VertexOutput vs_main( const VertexInput input ) 
{
    VertexOutput output;   

    output.position = mul(float4(input.position.xyz, 1.0f), worldViewProjectionMatrix); 
    
    output.texcoord = input.texcoord;
    output.worldPos = input.position;           // if you need untransformed vertex positions within your pixelshader
    output.eyePos   = inverseViewMatrix[3];     // if you need the players eye position (in world space)

    // return the fully initialized struct
    return pixel;
}
{% endhighlight %}


<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links to articles related to VertexShaders
[Techniques](/tutorials/hlsl-techniques#quicklink) :: [PixelShader](/tutorials/hlsl-pixelshader#quicklink)
</div> 