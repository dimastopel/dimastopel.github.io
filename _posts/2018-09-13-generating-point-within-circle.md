---
layout:     post
title:      Uniform point generation within circle
date:       2017-09-13 11:21:29
categories: general
math: true
---

So this is a problem that was bugging me for some time now and I never found a chance to hink about it thoroughly. The probem statement is simple: how to generate points within a circle in such a way that points' distribution be uniform? One can assume that a *rand()* function is provided and that it reurns a number betwen $0$ and $1$ with a uniform distribution. Once I investigated the problem in turned out being so facinating I decided to write a blog post about it. Here it is. 

For the sake of simplicity let's assume that the our curcle is a unit circle, i.e. a circle with radius $1$. 

The first solution that came into my mind was to generate an angle, between $0$ and $2\pi$, and a distance from the center between $0$ and $1$. Given specific andle $\alpha$ and distance $d$ we can generate a point using [polar coordinates](https://en.wikipedia.org/wiki/Polar_coordinate_system). To test this a created a small JavaScript program that generates $3000$ points within a circle. Here is what we get using the method above: 

<p align="center">
  <img src="/images/method_1.png" />
</p>

As you can see the distribution is far from uniform. There are much more points near the center than near the perimeter of the circle. Once you think about this, it is quite easy to prove that the distribution is indeed non uniform in this case. Let's assume some angle $\alpha$ that was already chosen and now we need to generate the distance $d$. There is a $0.5$ probability for $d$ to be greater than $0.5$ and same probability for it to be smaller. In other words there is a $0.5$ chance for the point to be within the circle with radius of $0.5$ and same chance for it to be outside of it. If you look at those two areas below it is clear their area is different. Therefore, given that we have similar number of points in each shows that the distribution is not uniform. 

<p align="center">
  <img src="/images/method_1_different_radii.png" />
</p>

In fact it is easy to show the difference in areas. The area with blue dots equals $$\pi \cdot (\frac{1}{2})^2 = \frac{\pi}{4}$$. The area with red dots equals $$\pi \cdot 1^2 - \frac{\pi}{4} = \frac{3}{4}\pi$$. So we have similar number of points (which converges to being equal as the number of points approaches infinity) in two areas with one *being $3$ times bigger than the other*. A clear non uniform distribution. 








Here is a formula: $e^{i\pi} + 1 = 0$ and so and so...

Now for another formula:

$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$

