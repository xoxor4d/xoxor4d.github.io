---
layout:     post
title:      "Introduction to custom CoD4-shaders"
date:       2020-01-01 23:59:00
categorie:  Call of Duty 4 - HLSL
permalink: /tutorials/hlsl-intro/
---
<div align="center" markdown="1">
#### If you have no idea what shaders can be used for, click one of the images below and see for yourself.   
I have a whole lot of other videos featuring hlsl shaders so go check them out if you are interested.
</div>

[![Play](/assets/img/tut_hlsl_yt_ao.jpg# left){: style="width: 32%"}](https://www.youtube.com/watch?v=GCxEoJcsv78) [![Play](/assets/img/tut_hlsl_yt_killstreak.jpg# left){: style="width: 32%"}](https://www.youtube.com/watch?v=WxhJXiDroO4) [![Play](/assets/img/tut_hlsl_yt_sky.jpg# left){: style="width: 32%"}](https://www.youtube.com/watch?v=vlulcpE3dgw)

---

# Introduction

Back in 2015, a guy called __Bear__ released his shader-linker that made it possible to add new hashed shader names to a shader-names-table the game uses to lookup shaders when linking fastfiles. 
The problem was that he did not specify how to setup the material so that the game could use these new shaders and with that, _no one used it as no one knew how to use it_.  

Link to the original post: [https://archive.raid-gaming.net/topic/1679-adding-new-sm3-hlsl-shaders-to-cod4/](https://archive.raid-gaming.net/topic/1679-adding-new-sm3-hlsl-shaders-to-cod4/)  
The full source-code he posted: [https://pastebin.com/4be66PEU](https://pastebin.com/4be66PEU)  

You'll need to know the .hlsl syntax and some basic understanding of how game/rendering engines work.  
If you need a quick overview, feel free to look around the following sites:

- General:
   + [http://rbwhitaker.wikidot.com/intro-to-shaders](http://rbwhitaker.wikidot.com/intro-to-shaders)
- Vertex Shader / Transformations / Matrix / Spaces:
   + [http://www.codinglabs.net/article_world_view_projection_matrix.aspx](http://www.codinglabs.net/article_world_view_projection_matrix.aspx)
- Pixel Shader / Texcoords ( UV´s ):
   + [https://www.3dgep.com/texturing-lighting-directx-11/](https://www.3dgep.com/texturing-lighting-directx-11/)

--- 

# Creating materials that use custom shaders

Material setup depends heavily on your shader use-case and can become quite tricky and messy.
The whole material chain depends on things like:

- use/sample textures within your shader?
- material use-case eg. hud elements, xmodels, skies or brushes?
- multiple shaders required for different lighting states?
- semanctic's needed for your shader?
- _the list goes on and on_ ...

<div align="right" markdown="1">
###### A quick overview of whats needed for any material in CoD4 to work.  
</div>  
![](/assets/img/tut_hlsl_intro_flow.jpg)

<div align="center" markdown="1">
#### Quick links for the individual files within the material chain with more in-depth information
[MaterialTemplates](/tutorials/hlsl-templates/) :: [Techsets](/tutorials/hlsl-techsets/) :: [Techniques](/tutorials/hlsl-techniques/) :: [Statemaps](/tutorials/hlsl-statemaps/) :: [PixelShader](/tutorials/hlsl-pixelshader/) :: [VertexShader](/tutorials/hlsl-vertexshader/)
</div>  

---
<div align="center" markdown="1">
We are going to create a scrolling 2D material, that can be used for eg. HUD-Elements, to be able to somewhat explain the setup thats needed.
#### This is obv. very basic but starting with something different would be way to much for this scope.
</div>  

# 1. Material Template > root\deffiles\materials
- create a copy of the closest template related to our use-case. Would be __mtl_2d.template__ in our case.
- asd

---






{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
