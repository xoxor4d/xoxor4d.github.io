---
layout:     post
title:      "Introduction to custom CoD4-shaders"
date:       2020-01-01 23:59:00
categorie:  Call of Duty 4 - HLSL
permalink: /tutorials/hlsl-intro/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/compileTools/header.jpg"; </script>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Table of Contents
[Introduction](#intro) :: [Overview](#creatematerials) :: [Material Templates](#templates) :: [Asset Manager](#assman)   
[Techset](#techset) :: [Technique](#technique) :: [Vertex Shader](#vertex) :: [Pixel Shader](#pixel) :: [Compiling Shaders / Download](#compiling) :: [Linking Shaders](#usingshader)
<div class="padding-2l"></div></div> 

<div align="center" markdown="1">
#### If you have no idea what shaders can be used for, click one of the images below and see for yourself.   
I have a whole lot of other videos featuring hlsl shaders so go check them out if you are interested.
<div class="padding-2l"></div>
</div>

[![Play](/assets/img/tut_hlsl_yt_ao.jpg# left){: style="width: 32%"}](https://www.youtube.com/watch?v=GCxEoJcsv78) [![Play](/assets/img/tut_hlsl_yt_killstreak.jpg# left){: style="width: 32%"}](https://www.youtube.com/watch?v=WxhJXiDroO4) [![Play](/assets/img/tut_hlsl_yt_sky.jpg# left){: style="width: 32%"}](https://www.youtube.com/watch?v=vlulcpE3dgw)



<!-- tag for quick links -->
<a name="intro"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# Introduction

Back in 2015, a guy called __Bear__ released his shader-linker that made it possible to add new hashed shader names to a shader-names-table the game uses to lookup shaders when linking fastfiles. 
The problem was that he did not specify how to setup the material so that the game could use these new shaders and with that, _no one used it as no one knew how to use it_.  

Link to the original post: [https://archive.raid-gaming.net/topic/1679-adding-new-sm3-hlsl-shaders-to-cod4/](https://archive.raid-gaming.net/topic/1679-adding-new-sm3-hlsl-shaders-to-cod4/)  
The full source-code he posted: [https://pastebin.com/4be66PEU](https://pastebin.com/4be66PEU)  

You need to know the .hlsl syntax and some basic understanding of how the DirectX 9 rendering-pipeline works.  
If you need a quick overview, feel free to look around the following sites:

- General:
   + [http://rbwhitaker.wikidot.com/intro-to-shaders](http://rbwhitaker.wikidot.com/intro-to-shaders)
- Vertex Shader / Transformations / Matrix / Spaces:
   + [http://www.codinglabs.net/article_world_view_projection_matrix.aspx](http://www.codinglabs.net/article_world_view_projection_matrix.aspx)
- Pixel Shader / Texcoords ( UV's ):
   + [https://www.3dgep.com/texturing-lighting-directx-11/](https://www.3dgep.com/texturing-lighting-directx-11/)


<!-- tag for quick links -->
<a name="creatematerials"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# Creating materials that use custom shaders

Material setup depends heavily on your shader use-case and can become quite tricky and messy.
The whole material chain depends on things like:

- Do you want to use/sample textures within your shader?
- Material use-case eg. hud elements, xmodels, skies or brushes?
- Multiple shaders required for different lighting states?
- Which shader-inputs do you need for your use-case?
- _The list goes on and on_ ...

<div align="right" style="padding-right: 3rem" markdown="1">
###### A quick overview of whats needed for any material in CoD4 to work.  
</div>  
![](/assets/img/tut_hlsl_intro_flow.jpg)

<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links for the individual files within the material chain with more in-depth information
[MaterialTemplates](/tutorials/hlsl-templates#quicklink) :: [Techsets](/tutorials/hlsl-techsets#quicklink) :: [Techniques](/tutorials/hlsl-techniques#quicklink) :: [Statemaps](/tutorials/hlsl-statemaps#quicklink) :: [PixelShader](/tutorials/hlsl-pixelshader#quicklink) :: [VertexShader](/tutorials/hlsl-vertexshader#quicklink)
</div>  


<div align="center" markdown="1">
We are going to create a scrolling 2D material, that can be used for eg. HUD-Elements, to be able to somewhat explain the setup thats needed.
#### This is obv. very basic but starting with something different would be way to much for this scope.
</div>  



<!-- tag for quick links -->
<a name="templates"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 1. Material Template > _root\deffiles\materials_

- Create a copy of the closest template related to our use-case. Would be __mtl_2d.template__ in our case.
- Name it __​z_scrolling_hud.template__

<div class="padding-1l"></div>

<div class="highlight-header"><p>mtl_2d.template</p></div>
{% highlight cpp %}
#include "commonsetup.template"
techniqueSet( "2d" ); // set the techset to use >> root\raw\techsets

textureTable
{
    #if "$colorMap$" == ""
        #error "colorMap may not be blank in 2d materials"
    #endif
    // This references our image as "material.colorMap" in the technique we are going to create later on >> root\raw\techniques
    "colorMap" = map( "@tileColor@", "@filterColor@", "$colorMap$", @nopicmipColor@ ) "@formatColor@" : "2d";
}
refImage( "$colorMap$" );
{% endhighlight %}

- This template fits perfectly, so all we need to change is the __techset__
- We are going to use this template only for this specific shader so we'll give the techset the same name as our template

<div class="highlight-header"><p>​z_scrolling_hud.template</p></div>
{% highlight cpp %}
#include "commonsetup.template"
techniqueSet( "z_scrolling_hud" );
/* ... */
{% endhighlight %}



<!-- tag for quick links -->
<a name="assman"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 2. Asset Manager

- ​Create a new material with the following settings:
- Compile it

<div class="padding-1l"></div>

{% highlight cpp %}
   + materialType : "custom"
   + blendFunc    : "Blend"
   + Template     : "z_scrolling_hud" ( the name of the template file we created in step 1 )
   + Color map    : "Input your Image" : "tile both*"
{% endhighlight %}


<!-- tag for quick links -->
<a name="techset"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 3. Techset > _root\raw\techsets_

- Search for __2d__ (the techset that was in the stock mtl_2d.template) and find __2d.techset__
- Create a copy, name it __z_scrolling_hud.techset__ and change it as follows:

<div class="padding-1l"></div>

<div class="highlight-header"><p>​2d.techset</p></div>
{% highlight cpp %}
"unlit":                // The lightstate / render technique ( 2d only uses unlit )
   vertcol_simple2d;    // This sets our technique >> root\raw\techniques
{% endhighlight %}

<div class="highlight-header"><p>​z_scrolling_hud.techset</p></div>
{% highlight cpp %}
"unlit":
   z_scrolling_hud;   // same name as the techset/material template (could be anything but we wont re-use any of the assets for other shaders)
{% endhighlight %}

<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Techsets in _root\raw\techsets_ will be used by GPUs running ShaderModel 3, but CoD4 also supports ShaderModel 2 so we have to 
create a copy of the new techset and place it in >> _​root\raw\techsets\sm2_ (a sm2 techset is needed or you'll get errors on linking your fastfile) 
</div>



<!-- tag for quick links -->
<a name="technique"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 4. Technique > _root\raw\techniques_

- Search for the technique __vertcol_simple2d.tech__ ( the original 2d one from the techset we used in step 3 )
- Create a copy and name it __z_scrolling_hud.tech__

<div class="padding-1l"></div>

<div class="highlight-header"><p>​vertcol_simple2d.tech</p></div>
{% highlight cpp %}
{
   stateMap "default2d";                       // Defines the statemap to use >> root\raw\statemaps
   vertexShader 1.1 "vertcol_simple.hlsl"      // Defines our vertex shader   >> root\raw\shader_bin\shader_src
   {
   }
	
   pixelShader 2.0 "vertcol_simple.hlsl"       // Defines our pixel shader    >> root\raw\shader_bin\shader_src
   {
      colorMapSampler = material.colorMap;     // Defines the Texture from our Material Template   >> root\deffiles\materials
   }
   vertex.position = code.position;            // Vertex Shader Input: Vertex Positions in local-space/model-space
   vertex.color[0] = code.color;               // Vertex Shader Input: Vertex Colors
   vertex.texcoord[0] = code.texcoord[0];      // Vertex Shader Input: Texcoords ( UV's in range 0.0f - 1.0f )
}
{% endhighlight %}

- Bear's shader-linker only works with ShaderModel 3 shaders, so change the version to __3.0__ (VertexShader and PixelShader) 
- Rename both shaders to __z_scrolling_hud__ and cut the __.hlsl__ extension
- Comment out __vertex.color[0] = code.color;__ because we are not going to use it in our shader (all defined inputs have to be used within the shader)

<div class="highlight-header"><p>​z_scrolling_hud.tech</p></div>
{% highlight cpp %}
{
   stateMap "default2d";
   vertexShader 3.0 "z_scrolling_hud"        // Defines our vertex shader   >> root\raw\shader_bin\shader_src
   {
   }
	
   pixelShader 3.0 "z_scrolling_hud"         // Defines our pixel shader    >> root\raw\shader_bin\shader_src
   {
      colorMapSampler = material.colorMap;
   }

   vertex.position = code.position;
   //vertex.color[0] = code.color;           // not needed
   vertex.texcoord[0] = code.texcoord[0];
}
{% endhighlight %}



<!-- tag for quick links -->
<a name="vertex"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 5. VertexShader > _root\raw\shader_bin\shader_src_

- The VertexShader only needs to transform our vertices into __worldViewProjectionSpace__  (cameraSpace)
- Create a new txt-file and call it: ___vs_3_0_z_scrolling_hud.hlsl__ (every custom VertexShader needs the "vs_3_0_" suffix)
- Paste the following:

<div class="padding-1l"></div>

<div class="highlight-header"><p>​vs_3_0_z_scrolling_hud.hlsl</p></div>
{% highlight cpp %}
#define PC                       // Needed for linker
#define IS_VERTEX_SHADER 1       // Needed for the shader compiler
#define IS_PIXEL_SHADER 0        // Needed for the shader compiler
#include <shader_vars.h>         // includes our global constants needed in every shader ( included within the download below )

struct VertexShaderInput         // This struct contains our vertex data input defined in our technique >> root\raw\techniques
{                                // This uses something called SEMANTICS (like a pipeline into the shader)
                                 // >> https://docs.microsoft.com/en-us/windows/desktop/direct3dhlsl/dx-graphics-hlsl-semantics

   float4 position : POSITION;   // float4 defines the size, in this case x,y,z,w; we define the semanctic POSITION as position
   float2 texCoord : TEXCOORD0;  // float2 because we only need x y on a 2d element; this is our UV in range 0.0 - 1.0
};

struct PixelShaderInput          // This struct will contain the vertex shader's output that the pixel shader will be using
{
   float4 position : POSITION;
   float2 texCoord : TEXCOORD0;
};


PixelShaderInput vs_main(VertexShaderInput input)  // Writing into the struct PixelShaderInput, using struct VertexShaderInput as input
{                                                  // Note that the function has to be called "vs_main"
   PixelShaderInput output;

   output.position = mul(float4( input.position.xyz, 1.0f), worldViewProjectionMatrix);
   // - This transforms our vertex positions from local-space to projection-/camera-space by multipling our vertices with a transformation Matrix
   // - Because we defined position as a float4, we also have to return a float4
   // - The "w" component is more or less the depth (distance from the camera), we don't use that on a 2d element -> so we use a scale of 1.0f

   output.texCoord = input.texCoord;
   // - We don't need to transform our UV's, so output = input

   return output;
   // - Return the fully initialized PixelShaderInput struct ("output")
}
{% endhighlight %}



<!-- tag for quick links -->
<a name="pixel"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 6. PixelShader > _root\raw\shader_bin\shader_src_

- The PixelShader will, as the name suggest, shade our pixels; 1 pixel at a time
- Create a new txt-file and call it: ___ps_3_0_z_scrolling_hud.hlsl__ (every custom PixelShader needs the "ps_3_0_" suffix)
- Paste the following:

<div class="padding-1l"></div>

<div class="highlight-header"><p>​ps_3_0_z_scrolling_hud.hlsl</p></div>
{% highlight cpp %}
#define PC
#define IS_VERTEX_SHADER 0
#define IS_PIXEL_SHADER 1
#include <shader_vars.h>

struct PixelShaderInput             // This is the output struct from our vertex shader 
{
   float4 position : POSITION;      // The SEMANTIC -> POSITION is not used within the pixel shader! But we still want to keep it here
   float2 texCoord : TEXCOORD0;
};

float4 ps_main(PixelShaderInput input) : COLOR     // As the pixelshader is only outputting a color, we link it to the SEMANTIC COLOR
{
   float4 output;                                  // Defining the variables we're going to be using 
   float  newX;                                    // These can be defined within the code itself, I just like to define them at the top 
	
   // horizontal scroll                      // Creating the scroll effect:
   newX = input.texCoord.x + gameTime.w;     // Add gameTime.w to our x-texcoord
                                             // gameTime.w increases linearly forever, and appears to be measured in seconds
                                             // ( now we get horizontal texcoords(x) above the 0-1 range                         )
                                             // ( if you would have set "tile both*" to "tile none" for your image in AssMan     )
                                             // ( the image would only draw as long as the texcoords are in range 0-1            )
                                             // ( anything above that would just be clipped of, thats how tiling textures work   )


   // tex2D() samples our texture with the given texture coordinates (UV's) and returns a colored pixel -> float4 color ( x,y,z,w or r,g,b,a )
   // function float4 tex2D() : tex2D(sampler, float2 texcoords)

   // Instead of input.texCoord (xy), we use our manipulated x-texcoord with the original y-texcoord: 
   output = tex2D(colorMapSampler, float2(newX, input.texCoord.y));
	
   // If you want a fixed alpha channel (in-case your texture doesn't have one) with half the transparency we could do:
      // output = float4( tex2D(colorMapSampler, float2(newX , input.texCoord.y)).rgb, 0.5 );

   // We could also manipulate the alpha afterwards by doing:
      // output = tex2D(colorMapSampler, float2(newX , input.texCoord.y));
      // output.w = 0.5;

   // return float4 "output" As COLOR
   return output;
}
{% endhighlight %}



<!-- tag for quick links -->
<a name="compiling"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 7. Compiling the shader so that cod-linker can access it

- Download the following package: [v1.1_hlsl_xoxor4d.zip](https://drive.google.com/open?id=14xNhEJtRVFaYG3rQZOV7fvjmd2R7CwUP) (includes all the files needed to compile your shaders)
- Copy the files within __2d_tutorial\additional_files__ into your cod4 root directory if you did all the above mentioned steps yourself
- Otherwise use the files within __2d_tutorial\whole_source__ (You still have to setup your material in Asset Manager as mentioned in Step 2)

<div class="padding-1l"></div>

- Go into __root\raw\shader_bin__
- Create a folder called __backups__ (the compiler will make a backup of your shader_names file every time you compile a shader)
- Type __cmd__ into the address-bar of your file-explorer window and hit enter to open a commandprompt that points to this directory

<div class="padding-1l"></div>
<div align="center" markdown="1">
Use the following to compile your shader: __shader_tool z_scrolling_hud__
</div>
<div class="padding-1l"></div>

- This will compile the Vertex- & Pixelshader using microsoft's fxc shader compiler
- Shader_tool will also add the hashed shader names to the shader_names file and copy the compiled binary shaders over into >> _root\raw\shader_bin_



<!-- tag for quick links -->
<a name="usingshader"></a>
<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# 8. Adding your custom material to your mod/map

- Now just do what you normally do when adding custom materials to your mod/map  
   (This is not different in any way. You don't need to include any files that we've created besides the material from Asset Manager.)

<div class="padding-1l"></div>

<div class="highlight-header"><p>​1. Zone File</p></div>
{% highlight cpp %}
material,z_scrolling_hud
{% endhighlight %}

<div class="highlight-header"><p>​2. GSC</p></div>
{% highlight cpp %}
precacheShader( "z_scrolling_hud" );   // Precache our material
/* ... */ 

self thread addHud( );
/* ... */ 

addHud( )
{
   self.shaderTest = newClientHudElem( self );
   
   self.shaderTest.x = 0;
   self.shaderTest.y = 0;
   self.shaderTest.alignX = "left";
   self.shaderTest.alignY = "middle";
   self.shaderTest.horzAlign = "center";
   self.shaderTest.vertAlign = "middle";

   self.shaderTest.sort = 1;
   self.shaderTest.alpha = 1.0;
   self.shaderTest.hideWhenInMenu = false;
   
   self.shaderTest setShader( "z_scrolling_hud", 64, 64 );
}
{% endhighlight %}

<div class="padding-1l"></div>

<div align="center" markdown="1">
Build your mod/map fastfile and put your __.iwi__ into your __.iwd__
# Run the game and test :)
</div>

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links for the individual files within the material chain with more in-depth information
[MaterialTemplates](/tutorials/hlsl-templates/) :: [Techsets](/tutorials/hlsl-techsets/) :: [Techniques](/tutorials/hlsl-techniques/) :: [Statemaps](/tutorials/hlsl-statemaps/) :: [PixelShader](/tutorials/hlsl-pixelshader/) :: [VertexShader](/tutorials/hlsl-vertexshader/)
</div>  