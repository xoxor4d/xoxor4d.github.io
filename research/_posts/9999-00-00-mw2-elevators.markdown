---
layout: post
title:  "Modern Warfare 2 - Elevators"
date:   2020-01-01 21:58:00
game:   "mw2"
permalink: /research/mw2-elevator/
---
>This won't explain how or why elevators work. This will only show you what was changed in order to prevent them in Modern Warfare 2.
>While trying to disable elevators in CoD4, I noticed that if I overjump a call to __PM_CorrectAllSolid__ or __PM_JitterPoint__ in later CoD's, elevators will stop working.
>I couldn't find anything special in that function and decided to compare it to the one in MW2 ... and well, Spot On!

<div class="padding-1l"></div>
<div align="center"><div class="seperator-75p"></div></div>
<div class="padding-1l"></div>

<div class="highlight-header"><p>PM_CorrectAllSolid - CoD4</p></div>
{% highlight cpp %}
bool PM_CorrectAllSolid(pmove_t *pm, pml_t *pml, trace_t *trace)
{
    /*Simplyfied Pseudocode*/
    while ( 1 )
    {
        point[0] = ps->origin[0] + (float)CorrectSolidDeltas[i][0];
        point[1] = ps->origin[1] + (float)CorrectSolidDeltas[i][1];
        point[2] = ps->origin[2] + (float)CorrectSolidDeltas[i][2];

        PM_playerTrace(pm, trace, ps->origin, pm->mins, pm->maxs, point, ps->clientNum, pm->tracemask)
        if ( !trace->startsolid )
            break;
      		
        i += 12;
        if ( i >= 312 )
        {
            ps->pm_flags &= 0xFFFFBFFF;
            ps->jumpOriginZ = 0.0f;
            GroundEntityNum = 1023;
            pml->groundPlane = 0;
            pml->almostGroundPlane = 0;
            pml->walking = 0;
            
            return 0;
        }
    }

    PM_playerTrace(pm, trace, ps->origin, pm->mins, pm->maxs, point, ps->clientNum, pm->tracemask)
    return true;
}
{% endhighlight %}  

<div class="highlight-header"><p>PM_CorrectAllSolid - MW2</p></div>
{% highlight cpp %}
bool PM_CorrectAllSolid(pmove_t *pm, pml_t *pml, trace_t *trace)
{
    /*Simplyfied Pseudocode*/
    while ( 1 )
    {
        point[0] = ps->origin[0] + (float)CorrectSolidDeltas[i][0];
        point[1] = ps->origin[1] + (float)CorrectSolidDeltas[i][1];
        point[2] = ps->origin[2] + (float)CorrectSolidDeltas[i][2];

        PM_playerTrace(pm, trace, ps->origin, pm->mins, pm->maxs, point, ps->clientNum, pm->tracemask)
        if ( !trace->startsolid )
        {
            /*some offsets on point*/
            PM_playerTrace(pm, trace, ps->origin, pm->mins, pm->maxs, point, ps->clientNum, pm->tracemask)
            if ( !trace->startsolid )
                break;
        }
            
      		
        i += 12;
        if ( i >= 312 )
        {
            ps->pm_flags &= 0xFFFFBFFF;
            ps->jumpOriginZ = 0.0f;
            GroundEntityNum = 1023;
            pml->groundPlane = 0;
            pml->almostGroundPlane = 0;
            pml->walking = 0;
            
            return 0;
        }
    }

    
    return true;
}
{% endhighlight %}

<div class="padding-2l"></div>

<div align="center" markdown="1">
#### All thats needed to re-enable elevators is to nop 1 jump equal instruction and the code-flow will be the same as it was in CoD4 :)
</div>


