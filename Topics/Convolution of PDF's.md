The key lies in the concept of convolution. If you convolve two rectangle functions, you will get a triangle function. Here we define the convolution of $f_X$ as

$$
(f_X * f_X)(x) = \int_{-\infty}^{\infty} f_X(\tau) f_X(x-\tau)\, d\tau.
$$

In fact, for any pair of random variables $X_1$ and $X_2$ (not necessarily uniform random variables), the sum $Z = X_1 + X_2$ will have a PDF given by the convolution of the two PDFs. We have not yet proven this, but if you trust what we are saying, we can effectively generalize this argument to many random variables. If we have $N$ random variables, then the sum $Z = X_1 + X_2 + \cdots + X_N$ will have a PDF that is the result of $N$ convolutions of all the individual PDFs.

- Summing $X+Y$ is equivalent to convolving the PDFs $f_X * f_Y$.
- If you sum many random variables, you convolve all their PDFs.


How do we analyze these convolutions? We need a second set of tools related to [[Fourier transforms]]. The Fourier transform of a PDF is known as the _characteristic function_, which we will discuss later, but the name is not important now. What matters is the important property of the Fourier transform, that a convolution in the original space is multiplication in the Fourier space. That is,

$$
\mathcal{F}\{(f_X * f_X * \cdots * f_X)\} = \mathcal{F}\{f_X\} \cdot \mathcal{F}\{f_X\} \cdot \cdots \cdot \mathcal{F}\{f_X\}.
$$

Multiplication in the Fourier space is much easier to analyze. In particular, for independent and identically distributed random variables, the multiplication will easily translate to addition in the exponent. Then, by truncating the exponent to the second order, we can show that the limiting object in the Fourier space is approaching a Gaussian. Finally, since the inverse Fourier transform of a Gaussian remains a Gaussian, we have shown that the infinite convolution will give us a Gaussian.

Here is some numerical evidence for what we have just described. Recall that the Fourier transform of a rectangle function is the sinc function. Therefore, if we have an infinite convolution of rectangular functions, equivalently, we have an infinite product of sinc functions in the Fourier space. Multiplying sinc functions is reasonably easy. See Figure 4.33 for the first three sincs. It is evident that with just three sinc functions, the shape closely approximates a Gaussian.

![Figure 4.33](https://probability4datascience.com/eBook/pix/ch4_sinc.png)

**Figure 4.33.** Convolving the PDF of a uniform distribution is equivalent to multiplying their Fourier transforms in the Fourier space. As the number of convolutions grows, the product is gradually becoming Gaussian.

How about distributions that are not rectangular? We invite you to numerically visualize the effect when you convolve the function many times. You will see that as the number of convolutions grows, the resulting function will become more and more like a Gaussian. Regardless of what the input random variables are, as long as you add them, the sum will have a distribution that looks like a Gaussian:

$$
X_1 + X_2 + \cdots + X_N \rightsquigarrow \mathrm{Gaussian}.
$$

We use the notation $\rightsquigarrow$ to emphasize that the convergence is not the usual form of convergence. We will make this precise later.

The implication of this line of discussion is important. Regardless of the underlying true physical process, if we are only interested in the sum (or average), the distribution will be more or less Gaussian. In most engineering problems, we are looking at the sum or average. For example, when generating an image using an image sensor, the sensor will add a certain amount of read noise. Read noise is caused by the random fluctuation of the electrons in the transistors due to thermal distortions. For high-photon-flux situations, we are typically interested in the average read noise rather than the electron-level read noise. Thus Gaussian random variables become a reasonable model for that. In other applications, such as imaging through a turbulent medium, the random phase distortions (which alter the phase of the wavefront) can also be modeled as a Gaussian random variable. Here is the summary of the origin of a Gaussian random variable:
