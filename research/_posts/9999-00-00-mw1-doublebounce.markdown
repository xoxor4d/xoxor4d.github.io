---
layout: post
title:  "CoD4 - Double Bounce"
date:   2020-01-01 23:59:00
game:   Call of Duty 4
permalink: /research/cod4-doublebounce/
---

There are 2 variables in the __playerState_s__ struct: __jumpOriginZ__ and __pm_flags__ that are assigned new values upon hitting the ground or a slope. These new values prevent __PM_StepSlideMove__ from executing specific parts of it that makes bouncing possible in the first place.

>   - jumpOriginZ
      + saves the max. z-origin for your current jump (current z-origin + jump_height dvar (probably for prediction))
      + the value gets saved till one hits a slope or a groundEntity and will get reset after around 2 seconds
>
>   - pm_flags
      + saves a flag, lets call it "Jumped-And-In-Air" ( 0x4000 ) when you perform a legit jump
      + the flag gets saved till one hits a slope or a groundEntity.

Lets assume we are on CoD4 and the current z-origin of the player is 1000.0f. The player is aiming for a bounce and at the moment he initiates the jump:  
 __jumpOriginZ__ contains __1039.0f__ ( z-origin (1000.0f) + jump_height (39)) and __pm_flags__ contains the __Jumped-And-In-Air__ flag.

Now if he hits the slope correctly, __PM_StepSlideMove__ will do its thing and initiate the bounce when __jumpOriginZ__ is higher then the current z-origin and if he still has the __Jumped-And-In-Air__ flag set. But with that, __PM_GroundTrace__ gets called from within __PM_StepSlideMove__ and resets these two variables in the playerState. These 2 values now prevent __PM_StepSlideMove__ from executing __PM_ProjectVelocity__ (the function responsible for bouncing).

Now to enable double bouncing, one has to disable the resets for these two variables within __PM_GroundTrace__ by nopping them (0x90). This will alter the flow of execution to a point where __PM_StepSlideMove__ thinks that the player just jumped, so it will always execute __PM_ProjectVelocity__.

{% highlight cpp %}
/*Part of PM_GroundTrace*/

if ( trace.walkable )
{
    pml->groundPlane = 1;
    pml->almostGroundPlane = 1;
    pml->walking = 1;

    if ( ps->groundEntityNum == 1023 )
        PM_CrashLand(pm, pml);

    ps->groundEntityNum = Trace_GetEntityHitId(&trace);
    PM_AddTouchEnt(pm, ps->groundEntityNum);
}
else
{
    ps->groundEntityNum = 1023;
    pml->groundPlane = 1;
    pml->almostGroundPlane = 1;
    pml->walking = 0;

    ps->pm_flags &= 0xFFFFBFFF; // would be the function Jump_ClearState(ps); // nop
    ps->jumpOriginZ = 0.0f;     // but its inlined in cod4                    // nop
}
{% endhighlight %}

There are obv. multiple ways of getting this to work. This way has some side effects like getting stuck on blockbounces or the slowdown-timer taking longer to reset. Latter happens because the slowdown-timer would normally start when one has hit the first bounce wherever now it starts counting down when the player walks on the ground.

Check out [MW2 Bouncing](/research/mw2-bounce/) for more info on how bounces work in general.
