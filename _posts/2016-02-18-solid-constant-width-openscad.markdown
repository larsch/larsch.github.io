---
layout: post
title:  "Solid of constant width in OpenSCAD"
date:   2016-02-18 21:10:05 +0100
categories: jekyll update
---

Here's a basic [OpenSCAD] script generating a model of a [solid of
constant width][socw-wiki] based on a tetrahedron. Now to figure out how to
position it with constant distance to the plane...

{% highlight scad %}
u = 10;
diameter = sqrt(8*u*u);
intersection() {
  translate([u,u,u]) sphere(diameter);
  translate([u,-u,-u]) sphere(diameter);
  translate([-u,u,-u]) sphere(diameter);
  translate([-u,-u,u]) sphere(diameter);
}
{% endhighlight %}

![Solid of constant width](/img/socw.png)



[![Numberphile Video on Shaps and Solids of constant width](http://img.youtube.com/vi/cUCSSJwO3GU/0.jpg)](http://www.youtube.com/watch?v=cUCSSJwO3GU "Shapes and Solids of Constant Width - Numberphile")

[socw-wiki]: https://en.wikipedia.org/wiki/Surface_of_constant_width
[OpenSCAD]: http://www.openscad.org/
