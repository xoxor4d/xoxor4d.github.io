---
layout: post
title:  "World at War - Mini Bounce"
date:   2020-01-01 22:58:00
game:   World at War
permalink: /research/waw-minibounce/
---
The fix for Bayonet-Jumps is also responsible for mini-bounces because they've just limited the maximum z-velocity a player can have instead of fixing the real issue.
3 new dvars were added: __player_bayonetLaunchDebugging__, __player_bayonetLaunchProof__ and __player_bayonetLaunchZCap__.


A check in __PM_MeleeChargeUpdate__ or __PM_MeleeChargeClear__, depending on your build, was added to check if __player_bayonetLaunchProof__ is enabled and if it is, limit the maximum z-velocity to the value stored in __player_bayonetLaunchZCap__.
This will act as a global z-velocity cap as that that function gets called every iteration of __PmoveSingle__.

So to fix mini bounces and also re-enable bayonetjumps, simply disable __player_bayonetLaunchProof__ or nop / invert the check in __PM_MeleeChargeUpdate__.

---

__PM_MeleeChargeClear__ (WaW / Bo1)
{% highlight cpp %}
void __cdecl PM_MeleeChargeClear(playerState_s *ps)
{
    ps->pm_flags &= 0xFFFDFFFF;
    ps->meleeChargeYaw = 0.0f;
    ps->meleeChargeDist = 0;
    ps->meleeChargeTime = 0;
  
    if ( player_bayonetLaunchProof->current.enabled )
    {
        if ((player_bayonetLaunchZCap->current.value - ps->velocity[2]) < 0.0f )
            ps->velocity[2] = *(float *)&player_bayonetLaunchZCap->current.integer;
    }
}
{% endhighlight %}