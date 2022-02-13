---
layout:         post
title:          "Call of Duty 4 :: Day and Night Cycle"
subtitle:       "with Film, Sun and Fog lerping ++ Volumetric Clouds"
description:    "Day and Night Cycle with Filmtweak, Lighttweak and Fog lerping ++ Volumetric Clouds, fully customizable in-game via the use of the IW3xo client"
date:           2021-07-03 00:00:00
permalink:      /projects/cod4-daynight/
image:          "/assets/img/daynight/thumb.jpg"
status:         "WIP - PUBLIC"
---
<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/daynight/header_c.jpg"; </script>
<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Quick Links
[GitHub Repository](https://github.com/xoxor4d/iw3xo-dev) :: [CoD4 Shader Tutorial](https://xoxor4d.github.io/tutorials/hlsl-intro/#compiling) :: [Discord Server](https://discord.gg/t5jRGbj)
<div class="padding-2l"></div></div> 

<div class="yt-container">
    <a href="https://www.youtube.com/watch?v=PlCpgC3jPcM">
        <img src="/assets/img/daynight/crash.jpg" class="yt-image">
        <img src="/assets/img/play_btn.png" class="yt-overlay">
    </a>
</div>

<div markdown="1" style="padding-left: 4rem; padding-right: 4rem;">

<div class="padding-2l" style="margin-top: -3.0rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>

<div class="padding-2l"></div>
<div class="padding-2l"></div>

# Overview
   + Built directly into IW3xo and fully tweakable via the in-game GUI :: [Pixel Shader](https://github.com/xoxor4d/xcommon_iw3xo/blob/master/src/raw/shader_bin/shader_src/ps_3_0_iw3xo_daynight.hlsl) :: [Day Night Cycle](https://github.com/xoxor4d/iw3xo-dev/blob/master/src/Components/Modules/DayNightCycle.cpp)
   + Filmtweak, Suntweak and Fogtweak lerping
   + 3 Time of Day states to lerp between
   + Config saving and loading
   + Sky shader based on: [https://github.com/lyubean/Godot-Sky-Clouds-shader-asset](https://github.com/lyubean/Godot-Sky-Clouds-shader-asset) :: ([MIT License](https://github.com/lyubean/Godot-Sky-Clouds-shader-asset/blob/master/LICENSE)) 

<div class="padding-2l"></div>
<div class="padding-2l"></div>

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>


![](/assets/img/daynight/gui01.jpg# halfsize left) ![](/assets/img/daynight/gui02.jpg# halfsize right) 
</div>

<div class="highlight-header"><p>Night example:</p></div>
![](/assets/img/daynight/crash_night.jpg# centered)

<div class="padding-2l" style="margin-top: -3.0rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

<div class="padding-2l"></div>

<div markdown="1" style="padding-left: 4rem; padding-right: 4rem;">
# Usage:
<div class="padding-1l"></div>
   1. Grab the latest [IW3xo Release](https://github.com/xoxor4d/iw3xo-dev/tags)
   2. Load up a map and use Devgui->DayNight to enable the day and night cycle
   3. Tweak to your heart's content

<div class="padding-2l"></div>

<div class="padding-2l" style="margin-top: -3.0rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

<div class="padding-2l"></div>

# GUI Settings In-Depth:
<div class="padding-2l"></div>
<div class="highlight-header"><p>General Settings</p></div>
{% highlight cpp %}
|-> Enable Time of Day Lerping          :: Enable lerping between time of day states.
|-> Enable Auto Sun Rotation            :: Automatically rotate the sun. Disable for manual mode using Sun Direction.
|-> Sun Direction                       :: r_lightTweakSunDirection (X) - position of the sun and thus, the lighting state.
|-> Day Length Scalar                   :: General day length scalar.
|-> Day Speed Scalar                    :: Speed up / Slow down daytime.
|-> Night Speed Scalar                  :: Speed up / Slow down nighttime.
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Cloud Settings (not all)</p></div>
{% highlight cpp %}
|-> Skydome Scale                       :: Cloud sphere size
|-> Cloud Coverage                      :: Amount of clouds
|-> Cloud Step Distance XZ              :: Distance scalar at which to draw "half-resolution" clouds
{% endhighlight %}

<div class="padding-2l"></div>
<div class="highlight-header"><p>Time of Day Settings</p></div>
{% highlight cpp %}
|-> Film Interpolation Speed            :: Time it takes to lerp to current filmtweak settings
|-> Sun Interpolation Speed             :: Time it takes to lerp to current lighttweak settings
|-> Tweak Fog                           :: Use custom fog settings for this state (uses default map settings otherwise)
{% endhighlight %}

<div class="padding-2l"></div>

<div align="center" style="margin-top: 1rem" markdown="1">
Config files are saved and loaded from:  
_root/iw3xo/daynight_
</div> 
</div>

<div class="padding-2l" style="margin-top: -3.0rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>

<div class="highlight-header"><p>Go completely crazy if you want:</p></div>
![](/assets/img/daynight/crash_crazy.jpg# centered)

<div class="padding-2l"></div>
