---
layout: post
title: Some fun equations
---

Because our app uses sound to exchange information, our app needs to be able to extract a sine with a given frequency out of a sum of sine’s. Our first idea was to use Fourier transform formula:

$$ F(v) = \int{-\infty}_{\infty} f(t)*e^{-ivt2\pi} dt $$

It is a formula that turns a function of time f(t) into a function of frequency F(v) but it was too intimidating and complex (lol), and we did not understand it. So we looked for alternatives which turned out to be the Fourier series of Fourier analysis:

To be continued...