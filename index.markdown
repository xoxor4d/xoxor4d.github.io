---
layout: page
title: "Overview / Projects"
---

# Site Migration - Incomplete
I didn't feel like paying for weebly any longer so I switched to github pages as it's more then enough for my use-case.
[Bouncepatch.com](https://bouncepatch.com) will redirect any requests to this site for the next year or so. This site will be frequently updated with tools / research / tutorials or whatever else I feel like is worth posting.

<div class="padding-1l"></div>
<div align="center"><div class="seperator-100p"></div></div>
<div class="padding-1l"></div>

# Current Projects
1. [IW3xo](/projects/iw3xo/) (eta. 2020) - custom CoD4 client with a multitude of new features including but not limited to:
   - __Interface__
	  + Improved main menu
	  + Improved in-game console ( eg. drag/resize with the cursor, console output when not using the fullscreen console, ... )
	  
   - __Visualization__ 
      + Draw Brushes with a specific material and/or only specific brushes (eg. draw clip brushes)
      + Visualize the players origin and/or velocity

   - __Movement__ 
      + Dvar tweakable movement types like _quake3/cpm_ or _cs:s/surf_
	  + Dvar tweakable stock movement settings

   - __FileSystem__
      + Load FastFiles Addons and IWDs on startup
	  + Live FastFile loading / unloading  


2. [CompileTools](/projects/cod4-compileTools/) (eta. 2020) - CoD4 compile tools with lots of improvements and new features including but not limited to:
	- __Interface__
	   + new ui using xaml
	   + changeable icons
	   + build in console output with text highlighting
	
	- __Features__
	   + auto copy fastfiles to _root/usermaps/_
	   + shader generator with a multitude of templates for view- / xmodels, hud elements and skies
	   + inject custom materials into stock weapon xmodels
	   + glsl -> hlsl syntax converter

<div align="center"><div class="seperator-100p"></div></div>
<div class="padding-1l"></div>

<div class="highlight-header"><p>Oh, .. hey there fellow</p></div>
{% highlight cpp %}
PM_CorrectAllSolid(pmove_t *pm, pml_t *pml, trace_t *trace)
{
	/* Simplyfied Pseudocode */
	while ( 1 )
  	{
    	PM_playerTrace(pmove_t *pm, trace_t *results, const float *start, const float *mins, const float *maxs, const float *end, int passEntityNum, int contentMask)
    	if ( !returned_value )
      		break;
      		
      	i += 12;
	    if ( i >= 312 )
	    {
	      	PM_FLAGS &= 0xFFFFBFFF;
	      	JumpOriginZ = 0.0;
	      	GroundEntityNum = 1023;
	      	*(_DWORD *)(a2 + 48) = 0;
	      	*(_DWORD *)(a2 + 52) = 0;
	      	*(_DWORD *)(a2 + 44) = 0;
	      	return 0;
	    }
  	}
  	PM_playerTrace(pmove_t *pm, trace_t *results, const float *start, const float *mins, const float *maxs, const float *end, int passEntityNum, int contentMask)
	result = 1;
	return result;
}
{% endhighlight %}

<div class="padding-1l"></div>

### Heading Level 3

> quote
idk
