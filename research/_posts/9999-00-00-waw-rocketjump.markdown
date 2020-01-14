---
layout: post
title:  "World at War - Rocketjumps"
date:   2020-01-01 22:59:00
game:   World at War
permalink: /research/waw-rocketjump/
---

<div align="center" markdown="1">
Rocketjumps happen in __Weapon_RocketLauncher_Fire__ and were fixed by not altering the z-velocity of the player if -weaponParms->forward[2] is > 0.0f.
</div>

<div class="highlight-header"><p>Part of Weapon_RocketLauncher_Fire - WaW</p></div>
{% highlight cpp %}
/* . . . */

if ( ent->client )
{
    upVec = wp->forward[2];
    
    if(-upVec > 0.0f)
        upVec = 0.0f;

    ent->client->ps.velocity[0] = gclient->ps.velocity[0] - wp->forward[0] * 64.0f;
    ent->client->ps.velocity[1] = gclient->ps.velocity[1] - wp->forward[1] * 64.0f;
    ent->client->ps.velocity[2] = gclient->ps.velocity[2] - upVec * 64.0f;
}

return result;
{% endhighlight %}

<div class="highlight-header"><p>Part of Weapon_RocketLauncher_Fire - CoD4</p></div>
{% highlight cpp %}
/*Part of Weapon_RocketLauncher_Fire*/

if ( ent->client )
{
    ent->client->ps.velocity[0] = gclient->ps.velocity[0] - wp->forward[0] * 64.0f;
    ent->client->ps.velocity[1] = gclient->ps.velocity[1] - wp->forward[1] * 64.0f;
    ent->client->ps.velocity[2] = gclient->ps.velocity[2] - wp->forward[2] * 64.0f;
}

return result;
{% endhighlight %}