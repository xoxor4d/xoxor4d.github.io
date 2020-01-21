---
layout: post
title:  "Modern Warfare 2 - Bouncing"
date:   2020-01-01 21:59:00
game:   "mw2"
permalink: /research/mw2-bounce/
---
# Some general info
Bouncing is possible via a combination of __PM_ProjectVelocity__ and __PM_StepSlideMove__. The latter function is needed for stairs and little elevations on the ground so the player doesn't
stop at every brush that is 1 unit heigher than the plane he is walking on. It basically lifts the player up if the brush he walks against is lower or equal the height thats set with the jump_stepSize dvar. 

>Fun Fact: CoD2 did not include __PM_ProjectVelocity__ and used __PM_ClipVelocity__ in its place. Hooking the call to __PM_ClipVelocity__ and instead calling your own version of __PM_ProjectVelocity__ will enable bouncing just like it is in CoD4.

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

# Bouncing in Modern Warfare 2
The Bouncefix that was first introduced in Modern Warfare 2 is just one check on a variable called __jumping__ right were it decides if __PM_StepSlideMove__ should return early or try to further clip/project the players origin/velocity. The __jumping__ variable was also set in CoD4's __PM_StepSlideMove__ but not used at that location.  

This snippet shows where __jumping__ is set for both games:

<div class="padding-1l"></div>

<div class="highlight-header"><p>​Part of PM_StepSlideMove - same for cod4 / mw2</p></div>
{% highlight cpp %}
if ( ps->pm_flags & 0x4000 && ps->pm_time )
    Jump_ClearState(ps);
    
if ( iBumps && ps->pm_flags & 0x4000 && Jump_GetStepHeight(ps, start_o, &fStepSize) )
{
    if ( fStepSize < 1.0 )
        return;

    jumping = 1;
}
{% endhighlight %}

Here you can see the change that prevents bouncing on MW2:
<div class="highlight-header"><p>Part of MW2's PM_StepSlideMove</p></div>
{% highlight cpp %}
if ( trace.fraction >= 1.0 )
{
    if ( fStepAmount != 0.0 )
        ps->origin[2] = ps->origin[2] - fStepAmount;
}
else
{
    if ( !trace.walkable && (jumping || trace.normal[2] < 0.30000001) ) // was :: if ( !trace.walkable && trace.normal[2] < 0.30000001 ) in cod4
    {
        ps->origin[0] = down_o[0];
        ps->origin[1] = down_o[1];
        ps->origin[2] = down_o[2];
        ps->velocity[0] = down_v[0];
        ps->velocity[1] = down_v[1];
        ps->velocity[2] = down_v[2];
        return;
    }

    Vec3Lerp(ps->origin, &in, trace.fraction, ps->origin);
    PM_ProjectVelocity(ps->velocity, trace.normal, ps->velocity);
}
{% endhighlight %}

<div class="padding-2l"></div>

<div align="center" markdown="1">
#### So removing that check re-enables bouncing like it was back in Call of Duty 4 :)
</div>

