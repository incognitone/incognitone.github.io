---
layout: post
title: Some fun equations
---

Because our app uses sound to exchange information, our app needs to be able to extract a sine with a given frequency out of a sum of sine's. Our first idea was to use Fourier transform formula:

$$ X(v) = \int_{-\infty}^{\infty} x(t) e^{-i 2 \pi v t}dt $$

It is a formula that turns a function of time f(t) into a function of frequency F(v) but it was too intimidating and complex (lol), and we did not understand it. So we looked for alternatives which turned out to be the Fourier series of Fourier analysis:

$$ f(x) = a_{0} + \sum (a_{n} cos (nx) + b_{n} sin (nx)) $$

with:

$$ a_{0} = \frac{2}{l} \int_{0}^{l} f(x)dx $$

$$ a_{n} = \frac{2}{l} \int_{0}^{l} f(x) * cos (nx) dx $$

$$ b_{n} = \frac{2}{l} \int_{0}^{l} f(x) * sin (nx) dx $$

Which is still a intimidating formula, but it basically means that any complex periodic function over a period L can be written as a sum of sine's and cosine's, the formula above turns such a function into the sum of all sine's and cosine's by just checking al frequencies and then it returns the amplitude of the frequency. All we need for our app is one frequency so we can just take the formula of bn with n being frequency * 2 * pi, if the value of b is above a certain threshold the function contains the frequency if it is not above the threshold the function does not contain the frequency.A big problem with this approach is that it does not work if there is a phase difference between the given function and sin(nx), a solution for this problem is trying different phase differences ortranslations, so sin(nx + tr) where tr is the translation. You put the function in a loop witch tries al tr from 0 to 2 * pi with steps of (2 * pi)/j where j is the accuracy. This solution does work but it is very time consuming which is a massive downside, so we decided to take another look at the Fourier transform formula, it does look like the formula for bn especially if you cleverly rewrite it like this:

$$ F(n) = \frac{2}{l} \int_{0}^{l} f(x) e^{inx}dx $$

Now the only difference is the e to the power i times nx instead of sin(nx). A little further researchshows that the output of the formula is a complex number with the magnitude being the amplitude and the angle being the phase of a given frequency. It takes the phase in to account which means that if we can get this function to work we don’t need the time consuming calculation of the phase difference. The question is what does the e to the power mean. By the use of Euler’s formula you can rewrite e to the power i times nx to:

$$ e^{inx} = cos(nx) + i * sin(nx) $$

If you spit the Fourier transform formula into its real and imaginary part you get:

$$ F_{r} = \frac{2}{l} \int_{0}^{l} f(x) * cos (nx) dx $$

$$ F_{i} = \frac{2}{l} \int_{0}^{l} f(x) * sin (nx) dx $$

To get the magnitude of a complex number you use the Pythagorean theorem, so to get the amplitude of frequency f you first convert f to n by multiplying by two pi than you put it in the readable version of the Fourier transform it gives you a real number and an imaginary number, you use the Pythagorean theorem:

$$ a = \sqrt{ F_{r}^{2} + F_{i}^{2} } $$

And BAM there is your amplitude.
