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

In fact it is easy to show the difference in areas. The area with blue dots equals $$\pi \cdot (\frac{1}{2})^2 = \frac{1}{4}\pi$$. The area with red dots equals $$\pi \cdot 1^2 - \frac{\pi}{4} = \frac{3}{4}\pi$$. So we have similar number of points (which converges to being equal as the number of points approaches infinity) in two areas with one *being $3$ times bigger than the other*. A clear non uniform distribution. 

So what is the *right* way? 

We should start by noticing that there should be more chance to generate a point if the $d$ is bigger. To demonstrate this please see the image below. To have uniform distribution we need to to be able to generate more points for larger $d$ - blue points in the image below, and less points for smaller $d$ - red points in the image below. 

<p align="center">
  <img src="/images/method_2_red_blue_dots.png" />
</p>

It is clear that the number of dots correlates with the circumference of a circle with radius $d$. The larger the $d$ the larger the circumference, the more dots we need to be able to generate there to keep uniform distribition. The lenght of the circumference of a circle given $d$ is $2\pi d$, so the relation beween $d$ and circumference is *linear*. Thus the relation between $d$ and the number of dots with radius equal to $d$ is linear. Given this we can create a [probability density function](https://en.wikipedia.org/wiki/Probability_density_function) (PDF) for a range of $d$ between $0$ and $1$. We know that the *x* axis is defined to be between $0$ and $1$. We know that for $d$ the probability should be $0$. We also know that the function is linear. Given that the area under PDF must equal $1$ we get the following function: 


Now we need a way to generate random numbers based on this PDF. How do we do it? Fortunately there is a method for this called [inverse transform sampling](https://en.wikipedia.org/wiki/Inverse_transform_sampling). The method consists of the following $3$ steps: 

1. Create [cumulative distribution function](https://en.wikipedia.org/wiki/Cumulative_distribution_function) (CDF) from PDF  
2. Find an [inverse function](https://en.wikipedia.org/wiki/Inverse_function) to a CDF you have found in the previous step 
3. Generate regular uniformly distributed numbers and transform them through the inverse function from step $2$. The resulting numbers will have the probability distribution as the original one

Let's do it. Our *PDF* is $$PDF(x)=2x$$. *CDF* is an integral of *PDF*. Therefore:

$$CDF(x) = \int PDF(x)dx = \int 2x dx = x^2$$  

Now we need to find the inverse function for *CDF(x)*. But it is clear. The inverse of a square is square root. So the inverse of *CDF* is $$InvCDF(x)=\sqrt{x}$$.

Now, if we generate numbers with uniform distribution and find a square root of each we will get numbers that behave as we want. To recap, what we need to do now is to generate $\alpha$ as we did previously, then generate $d$ but before using $d$ apply a square root on it. If we do this we receive the following distributin: 

<p align="center">
  <img src="/images/method_2_final.png" />
</p>



Here is a formula: $e^{i\pi} + 1 = 0$ and so and so...

Now for another formula:

$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$


 primes 1 100 |gnuplot -p -e 'plot "/dev/stdin"