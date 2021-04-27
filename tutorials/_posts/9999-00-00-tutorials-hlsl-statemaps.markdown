---
layout:     post
title:      "In-depth :: Statemaps"
subtitle:   ">> root\\raw\\statemaps"
date:       2020-01-01 23:56:00
categorie:  Call of Duty 4 - HLSL
permalink: /tutorials/hlsl-statemaps/
---

<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/compileTools/header.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>


<div align="center" markdown="1">
Statemaps use a switch-case syntax and are used to define effect-states for the current technique pass. Statemaps can fixate states, overwrite states,  
define default values if no matching condition was found or simply pass the value that was set for the material in AssetManager.  

<div class="padding-1l"></div>

Statemaps and their names are pretty self-explanatory so I wont go into much detail here.  
I advice to not alter any stock statemaps. Create copies of them and change the name within your technique instead.

<div class="padding-1l"></div>
<div class="seperator-75p"></div>
</div>

<div class="padding-1l"></div>

<div class="highlight-header"><p>default_alpha.sm (custom)</p></div>
{% highlight cpp %}
alphaTest
{
    mtlAlphaTest == Always && mtlBlendOp == Add && mtlSrcBlend == SrcAlpha && mtlDestBlend == InvSrcAlpha:  // if values in AssetManager
    mtlAlphaTest == Always && mtlBlendOp == Add && mtlSrcBlend == SrcAlpha && mtlDestBlend == One:          // if values in AssetManager
        GT0;                                                                                                // assign GT0 to multiple cases
	
    default:            // overwise
        passthrough;    // use the value set in AssetManager
}

blendFunc
{
    default:
        Add, SrcAlpha, One;
}

separateAlphaBlendFunc
{
    default:
        Disable, One, Zero;
}

cullFace
{
    default:
        passthrough;
}

depthTest
{
    default:
        passthrough;
}

depthWrite
{
    default:
        Enable;
}

colorWrite
{
    default:
        Enable, Enable;
}

polygonOffset
{
    default:
        passthrough;
}

stencil
{
    default:
        passthrough;
}

wireframe
{
    default:
        Disable;
}
{% endhighlight %}


<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div align="center" markdown="1">
#### Quick links to articles related to Statemaps
[Techniques](/tutorials/hlsl-techniques#quicklink)
</div> 