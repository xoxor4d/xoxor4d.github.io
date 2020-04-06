---
layout:         post
title:          "Call of Duty 4 :: IW3xRadiant"
subtitle:       "A CoD4 Radiant Modification"
description:    "A CoD4 Radiant Modification built to be used with IW3xo. Live-Link between CoD4 and Radiant. Features brush/camera synchronization, dvar manipulation ..."
date:           2020-04-04 00:00:00
permalink:      /projects/iw3xo-radiant/
image:          "/assets/img/vid-live-link.jpg"
status:         "WIP - PUBLIC"
---
<!-- overwrite header bg if defined -->
<script> var header_bg = "/assets/img/iw3xo-radiant/header.jpg"; </script>

<!-- tag for quick links so we do not show the nav -->
<a name="quicklink"></a>

<div align="center" style="margin-top: -1rem" markdown="1">
#### Quick Links
[GitHub Repository](https://github.com/xoxor4d/iw3xo-radiant) :: [Latest Release](https://github.com/xoxor4d/iw3xo-radiant/releases) :: [IW3xo](/projects/iw3xo/)
<div class="padding-2l"></div></div> 

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l" style="margin-bottom: -0.5rem"></div>

<div class="padding-1l"></div>
![](/assets/img/iw3xo-radiant/link02.jpg) 

<div class="padding-1l"></div>
![](/assets/img/iw3xo-radiant/link01.jpg) 

<div class="padding-1l"></div>
![](/assets/img/iw3xo-radiant/link03.jpg) 

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>

<div markdown="1" style="padding-left: 2rem">
# Features
<div class="padding-2l"></div>
__Interface__
   + Minor UI modifications
   + External I/O Console with built in commands:
     - getdvar \<_dvarName_>
     - setdvar \<_dvarName_> <_value/s_>
<div class="padding-2l"></div>
__Config__ 
   + Implemented config save/load code (dvars)
   + Config file __iw3r.cfg__ will be loaded and executed on init
   + Config will be generated when closing radiant
   + Added new dvars to control live-link:
     - radiant_live
     - radiant_liveDebug
     - radiant_livePort
<div class="padding-2l"></div>
__Live-Link__ 
   + Live-Link is enabled by default and searches for a compatible server on __localhost:3700__ (default port)
   + Radiant will automatically connect once it finds a server
   + Live-Link features:
     - Synchronize worldspawn settings (sundirection, suncolor, sunlight) by setting equivalent "r_lighttweak" dvars in-game
     - Set dvars on the server (^)
     - Send text messages to the server
     - Synchronize up to 16 selected brushes with the server
     - Synchronize cameras (__radiant \-> server__, __server \-> radiant__ or __both__)
<div class="padding-2l"></div>
__Misc__
   + Removed console spam on init
   + Fixed a few issues with heavy custom-shader usage
   + Fixed "black world" upon selecting a brush with sunlight-preview enabled (only disables sunlight-preview now)
</div>

<div class="padding-2l" style="margin-top: -2.5rem"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-2l" style="margin-bottom: -0.5rem"></div>

[![Play](/assets/img/vid-live-link.jpg# left){: style="width: 50%"}](https://www.youtube.com/watch?v=SBqZLfCaRdw) [![Play](/assets/img/vid-map-export.jpg# right){: style="width: 50%"}](https://www.youtube.com/watch?v=UOjiakKrNdk)