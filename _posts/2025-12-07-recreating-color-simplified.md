---
title: "Simplified Color Recreation Theory for Modern Displays"
date: 2025-12-07 16:00:00 -0700
tags: [photography, physics]
math: true
---

Real world colors are continous spectra, such as the [sunlight spectrum](https://en.wikipedia.org/wiki/Sunlight#Composition_and_power). We can discribe it as a continous function $J(\lambda)$ where $\lambda$ is the wavelength and $J(\lambda)$ is the intensity at that wavelength.

Human eyes have three types of color receptors (cone cells) that are [sensitive to different ranges of wavelengths](https://en.wikipedia.org/wiki/LMS_color_space), with name L, M, S for long, medium and short wavelengths respectively, loosely corresponding to red, green and blue colors. Represent the responsiveness of these three types of cells as functions $s(\lambda)$ at wavelength $\lambda$, then the perceived intensity of a type of cone cell can be expressed as (take L as an example):

$$
L = \int_0^\infty J(\lambda) s_L(\lambda) d\lambda
$$

and same goes for M and S cells. As long as $\begin{bmatrix} L & M & S \end{bmatrix}$ are the same, the perceiption will be the same. It is significant not only because it is the basis of human color vision, but also because camera sensors, utilizing [Bayer filter](https://en.wikipedia.org/wiki/Bayer_filter) or similar technologies, also mimic this mechanism to capture colors.

It can be noted that for the same perceived color (fixed $\begin{bmatrix} L_0 & M_0 & S_0 \end{bmatrix}$), there are infinite possible spectra $J(\lambda)$ that can produce the same perception. This is called [metamerism](https://en.wikipedia.org/wiki/Metamerism) which enables modern displays to reproduce or approximate colors with a spectra different from the real world ones. It is also, in fact, true that modern displays (such as LCD, OLED, etc.) works by exploiting this method, namely, they have three kinds of primary color lights red, green and blue that has artificial but fixed spectra, and the ability to adjust the intensity of each primary color. Namely, let $r$, $g$ and $b$ be the intensities of the RGB lights respetively (which happens to be the RGB values we usually read in digital images) and let $J_R(\lambda)$, $J_G(\lambda)$ and $J_B(\lambda)$ be the fixed, artificial spectra of the RGB lights, the overall spectrum emitted by the display can be expressed as:

$$
J_\text{display}(\lambda) = r J_R(\lambda) + g J_G(\lambda) + b J_B(\lambda)
$$

Consider one kind of cone cell, say L, to recreate $L_0$, we have:

$$
\begin{align*}
L_0 &= \int_0^\infty J_\text{display}(\lambda) s_L(\lambda) d\lambda \\
    &= \int_0^\infty \left( r J_R(\lambda) + g J_G(\lambda) + b J_B(\lambda) \right) s_L(\lambda) d\lambda \\
    &= r \int_0^\infty J_R(\lambda) s_L(\lambda) d\lambda + g \int_0^\infty J_G(\lambda) s_L(\lambda) d\lambda + b \int_0^\infty J_B(\lambda) s_L(\lambda) d\lambda
\end{align*}
$$

Notice how $L_0$ is a linear conbination of $\int_0^\infty J_R(\lambda) s_L(\lambda) d\lambda$, $\int_0^\infty J_G(\lambda) s_L(\lambda) d\lambda$ and $\int_0^\infty J_B(\lambda) s_L(\lambda) d\lambda$ with coefficients $r$, $g$ and $b$. These integrals are named as sensitivities of the display primaries to the L cone cell, denoted as $S_{L,R}$, $S_{L,G}$ and $S_{L,B}$ respectively. Thus, we can represent the color recreation for L, M and S cone cells in matrix form regarding the sentivities $\mathbf{S}$:

$$
\begin{bmatrix}
L \\
M \\
S
\end{bmatrix} 

= 
\begin{bmatrix}
S_{L,R} & S_{L,G} & S_{L,B} \\
S_{M,R} & S_{M,G} & S_{M,B} \\
S_{S,R} & S_{S,G} & S_{S,B}
\end{bmatrix}
\begin{bmatrix}
r \\
g \\
b
\end{bmatrix}
$$

in which case, to recreate the perceiption of $\begin{bmatrix} L_0 & M_0 & S_0 \end{bmatrix}$, we only need to calculate:

$$
\begin{bmatrix}
r \\
g \\
b
\end{bmatrix}
=
\mathbf{S}^{-1}
\begin{bmatrix}
L_0 \\
M_0 \\
S_0
\end{bmatrix}
$$

And sometimes, the values of $r$, $g$ and $b$ may exceed the display's capability (for example, negative values or values larger than the maximum intensity), in which case we need to go creative with color management techniques such as [gamut mapping](https://en.wikipedia.org/wiki/Gamut_mapping) to find the best approximate color that the display can produce.
