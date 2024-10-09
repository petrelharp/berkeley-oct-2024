---
title: "Forwards and backwards in spatially heterogeneous populations"
author: "Peter Ralph"
date: "Probability Seminar <br/> UC Berkeley // 9 October 2024"
---

# Outline

<!--
title-slide-attributes:
    data-background-image: /path/to/title_image.png
    data-background-size: contain
-->

::: {.columns}
:::::: {.column}

**Joint work with:**

- Alison Etheridge (Oxford)
- Tom Kurtz (Madison)
- Ian Letter (ex-Oxford)
- Terence Tsui (Warwick)

:::
:::::: {.column width=50%}

![](figs/coauthors.png)

:::
::::::

-----------

[![Looking forwards and backwards: Dynamics and genealogies of locally regulated populations](figs/paper_header.png)](https://dx.doi.org/10.1214/24-EJP1075)


*slides:* [github.com/petrelharp/berkeley-oct-2024](https://petrelharp.github.io/berkeley-oct-2024/berkeley-oct-2024.slides.html)


--------------------

> UO is located on the traditional indigenous homeland of the Kalapuya people.
Kalapuya people were dispossessed of their indigenous homeland by the United States government and forcibly removed.
Today, Kalapuya descendants are primarily citizens of the Confederated Tribes of Grand Ronde and the Confederated Tribes of Siletz Indians,
and continue to make important contributions to their communities, to the UO, to Oregon, and to the world.


# Motivation


## Motivating question

::: r-stack

:::: {.fragment .coverup}
> What can we deduce about the history of a population from
patterns of genetic variation that we observe today?
::::

:::: {.fragment .coverup}
> What can we deduce about the <span class="blue">geographic</span> history of a population from
patterns of genetic variation that we observe today?
::::

:::: {.fragment .coverup}
> What can we deduce about the <span class="blue">geographic</span> of a population from
the <span class="red">genealogies</span> that we observe today?
::::

:::

::::: fragment
![trees in space](figs/locator_spatial_tree_sequence.png){width=70%}

:::{.caption}
*image by CJ Battey*
:::
::::::


--------

::: {.columns}
:::::: {.column width=50%}

How we usually model space:

![](figs/lawn.png)


*"Over large spatial and temporal scales local details should wash out"*

:::
:::::: {.column width=50%}

:::: fragment
*... but will they?*

![Drummond's anemone](figs/flower.png)
::::

:::
::::::

## The world is not flat (or, homogeneous) {data-background-image="figs/east_bay.jpg" data-background-position=center}

::: r-stretch

:::


# A model

## A model, based on "interacting branching processes"

:::: {.columns}
:::::: {.column width=60%}

$$\eta(x) = \text{population at (or close to) } x$$

::: incremental 
- A juvenile is born <span class="fragment blue">*per capita rate $\gamma(x, \eta(x))$*</span>
- Dispersal <span class="blue fragment">*distribution $q(x, dy)$ (Gaussian)*</span>
- Establishment <span class="blue fragment">*probability $r(y, \eta(y))$*</span>
- Death of mature individuals <span class="blue fragment">*rate $\mu(x, \eta(x))$*</span>
:::

::: fragment
Can choose functional forms to achieve stability.
:::


::::
:::::: {.column width=40%}

::: r-stack 

::::: fragment
![A newly established plant](figs/established_plant.jpg){width=90%}
:::::

::::: fragment
![A kid about to blow seeds off a flower head](figs/dispersal.png)
:::::

::::: fragment
![A newly established plant](figs/established_plant.jpg){width=90%}
:::::


:::

::::
::::::

::: {.fragment .highlight-red}
*We only track mature individuals.*
:::


# A note of caution

::: {.floatright}
![Gilia Patterson](figs/gilia.jpeg){width=40%}

::::: {.caption}
*Gilia Patterson*
:::::

:::


---------------------

::: {.columns}
:::::: {.column width=60%}

- death: $\mu = 0.3$ per time step

- establishment: $r = 0.7$

- dispersal: Gaussian with SD $\sigma$

- local density: in circle of radius $\epsilon$

- reproduction: with $K=1$, $\lambda=3$,
$$ \gamma = \frac{\lambda}{1 + \text{(local density)}/K} $$

- non-spatial 'equilibrium density':
$$ K \left( \frac{\lambda}{1 - r} - 1 \right) .$$

:::
:::::: {.column width=40%}

![screenshot of SLiM GUI](figs/slim_screenshot.png)

::: {.caption}
*SLiM code at [github.com/petrelharp/berkeley-oct-2024](https://github.com/petrelharp/berkeley-oct-2024/raw/main/gilia_clumping_sim.slim)*
:::

:::
::::::


## Large dispersal distance

-  dispersal distance $\sigma = 3$
-  interaction distance $\epsilon = 1$
-  mean # offspring $\propto (1 + \text{(density)} / K)^{-1}$

. . .

![not patchy](figs/gilia_high_sigma.png)

## Small dispersal distance

-  dispersal distance $\sigma = 0.2$
-  interaction distance $\epsilon = 1$
-  mean # offspring $\propto (1 + \text{(density)} / K)^{-1}$


![not patchy](figs/gilia_low_sigma.png)

. . .

Low dispersal distance compared to distance over which negatively influenced by presence of neighbors
can lead to strong clumping - <span class="fragment">true even in deterministic model! 
*[(Sasaki 1997)](https://doi.org/10.1006%2Fjtbi.1996.0370)*</span>


# Characterising the model

## Local density

Birth-death process with dynamics:

- A juvenile is born <span class="blue">*per capita rate $\gamma(x, \eta(x))$*</span>
- Dispersal <span class="blue">*distribution $q(x, dy)$ (Gaussian)*</span>
- Establishment <span class="blue">*probability $r(y, \eta(y))$*</span>
- Death of mature individuals <span class="blue">*rate $\mu(x, \eta(x))$*</span>

. . .

::: red
Think of population as a point measure, with atoms of mass $1/N$,
and write
$$ \langle f, \eta \rangle = \frac{1}{N} \sum f(X_i) = \int f(x) \eta(dx) . $$
:::

. . .

::: blue
Rates depend on *local density near $x$*:
$$ \gamma(x, \eta(x)) := \gamma(x, \rho_\gamma * \eta(x));
\qquad \rho_\gamma * \eta(x) = \int \rho_\gamma(x-y) \eta(dy) .$$
:::

. . .

There are *three* interaction kernels, $\rho_r$, $\rho_\gamma$, and $\rho_\mu$,
which need not be the same.


## Scaling the model  -- <span class="red">parameters $N$, $\theta \to \infty$</span>

Birth-death process with dynamics:

- A juvenile is born per capita rate ${\color{red}\theta}\gamma(x, \eta(x))$
- Dispersal distribution $q_{\color{red}\theta}(x, dy)$ (Gaussian <span class="red">mean and variance order $1/\theta$</span>)
- (Instantaneous) establishment probability $r(y, \eta(y))$
- Death of mature individuals rate ${\color{red}\theta}\mu_{\color{red}\theta}(x, \eta(x))$

. . .

Assume: 
$$ \theta\left( r(x, \eta) \gamma(x, \eta) - \mu_\theta(x, \eta)\right) = F(x,\eta)$$

. . . 

$$\int \theta\left( r(z, \eta) f(z) - r(x,\eta)f(x) \right) q_\theta(x, dz)
\stackrel{\theta\to\infty}{\longrightarrow} \Delta\left(r(\cdot, \eta) f(\cdot)\right)(x) $$

. . .

::: tiny
(Roughly, $r$ sufficiently smooth and net per capita growth rate $\propto 1/\theta$.)
:::

. . .

See paper for more general case:
inhomogeneous diffusion instead of $\Delta$.


## How do things change, locally? <span class='smallish'>$\langle f, \eta \rangle = \frac{1}{N} \sum f(X_i) = \int f(x) \eta(dx)$</span>

::: incremental
- Individual at $x$ gives birth to a single mature offspring at $z$ at rate
$$ \color{blue}{\theta \gamma(x, \eta) q_\theta(x,dz) r(z, \eta)} \qquad \color{red}{\text{increment } \langle f,\eta \rangle \text{ by } \frac{1}{N} f(z)}$$

- Individual at $x$ dies at rate 
$\qquad \color{blue}{\theta\mu_\theta(x,\eta)} \qquad \color{red}{\text{increment } \langle f,\eta \rangle \text{ by } -\frac{1}{N} f(x)}$
:::

. . .


$$\begin{aligned}
\frac{d}{dt}\mathbb{E}\left[\langle f, \eta_t\rangle \big| \eta_0 = \eta\right] \big|_{t=0} 
\hspace{20em}
\end{aligned}$$

::: r-stack

:::: {.fragment .coverup}
$$\begin{aligned}
&\qquad = \theta \int \int \color{red}{\frac{1}{N}} f(z) r(z, \eta) 
q_\theta(x, dz) \gamma(x, \eta) \color{red}{N} \eta(dx) 
\\ &\qquad \qquad \qquad 
- \theta \int \color{red}{\frac{1}{N}} f(x) \mu_\theta(x, \eta) \color{red}{N} \eta(dx) .
\end{aligned}$$
::::

:::: {.fragment .coverup}
$$\begin{aligned}
& = \theta \int \int f(z) r(z, \eta) q_\theta(x, dz)\gamma(x, \eta) \eta(dx)
- \theta \int f(x) \mu_\theta(x, \eta)\eta(dx) \\
&\vphantom{\int}
\end{aligned}$$
::::

:::: {.fragment .coverup}
$$\begin{aligned}
 &= \int \left( \int \theta(f(z) r(z, \eta) - f(x) r(x, \eta)) q_\theta(x,dz)\right) \gamma(x, \eta) \eta(dx) \\
 &\qquad \qquad {}+ \int f(x) \theta \left(r(x,\eta)\gamma(x, \eta) - \mu_\theta(x,\eta)\right) \eta(dx) .
\hspace{5em}
\end{aligned}$$

<!--
::: floatright
<span class="red">using $\int q_\theta(x,dz) = 1$</span>
:::
-->
::::

:::

:::: fragment
$$
\stackrel{\theta \to \infty}{\longrightarrow}
\int \gamma(x,\eta) \Delta(f(\cdot)r(\cdot,\eta))(x) \eta(dx)
+ \int f(x) F(x,\eta) \eta(dx)
$$
::::

## Quadratic variation

- Individual at $x$ gives birth to single mature offspring at $z$ at rate
    <span class="blue">$\theta \gamma(x,\eta)r(z,\eta)q_\theta(x,dz)$:</span>
    <span class="red">increment $\langle f, \eta \rangle = \frac{1}{N} f(z)$</span>

- Individual at $x$ dies at rate
    <span class="blue">$\theta \mu_\theta(x,\eta)$:</span>
    <span class="red">increment $\langle f, \eta \rangle = -\frac{1}{N} f(x)$</span>

$$\begin{aligned}
& \theta \big\{ \int \int \frac{1}{N^2} f^2(z) r(z,\eta) q_\theta(x,dz) \gamma(x,\eta) N \eta(dx)
\\&\qquad \qquad {} +
\int \frac{1}{N^2} f^2(z) \mu_\theta(x,\eta) N \eta(dx) \big\}
\\&\qquad = \frac{\theta}{N} \int
\left\{ \int f^2(z) r(z,\eta) q_\theta(x,dz) \gamma(x,\eta) + f^2(x) \mu_\theta(x,\eta) \right\} \eta(dx)
\end{aligned}$$

::: {.fragment .red}
$$
\int f^2(z) r(z,\eta) q_\theta(x,dz) \to f^2(x) r(x,\eta),
\qquad
\mu_\theta = r\gamma - \frac{1}{\theta}F \to r \gamma
$$
:::

::: fragment
$$\hspace{10em}\color{blue}{
\stackrel{\theta\to\infty}{\longrightarrow} \alpha \int 2 r(x,\eta) \gamma(x,\eta) f^2(x) \eta(dx) }
\qquad \text{where }
\color{red}{ \alpha := \lim \frac{\theta}{N} }
$$
:::

## small / large $\theta$:

![Snapshot of a simulation showing smooth distribution of indivdiuals](figs/fig1a.png){width=45%}
![Snapshot of a simulation showing patchy distribution of indivdiuals](figs/fig1b.png){width=45%}

## Martingale characterization of limit

$$\begin{aligned}
& \langle f(x), \eta_t(dx)\rangle - \langle f(x), \eta_0(dx)\rangle
\\&\qquad {} 
- \int_0^t \big\langle \gamma(x,\eta_s)\Delta\left(f(\cdot)r(\cdot,\eta_s)\right)(x) + F(x,\eta_s)f(x),
    \eta_s(dx) \big\rangle ds
\end{aligned}$$
is a martingale, $M_f(\cdot)$, with conditional quadratic variation
$$ \langle M_f \rangle_t = \alpha \int_0^t \big \langle 2 r(x,\eta_s)\gamma(x,\eta_s) f^2(x), \eta_s(x) \big \rangle ds . $$


::: incremental
- $\alpha=\lim \frac{\theta}{N} =0$: non-local PDE <span class="blue fragment">(since $\gamma(x,\eta_s) = \gamma(x,\rho_\gamma*\eta_s(x))$)</span>
- can also recover 'local' PDEs $$\partial_t \eta = r \Delta(\gamma \eta) + F\eta$$
- $\alpha > 0$: nonlinear superprocess
:::

. . .

e.g., $\gamma\equiv1$, $r\equiv1$, $F=1-\rho*\eta$, (diffusion limit of) Bolker-Pacala model: spatial branching process; reproductive success decreases in crowded regions.

## Assumptions

Assume

$$\int \theta(f(z) r(z, \eta) - f(x) r(x, \eta)) q_\theta(x,dz)
\stackrel{\theta \to \infty}{\longrightarrow}
\Delta(f(\cdot)r(\cdot,\eta))(x)$$

$$\theta\left(
r(x,\eta) \gamma(x,\eta) - \mu_\theta(x,\eta)
\right) = F(x,\eta)$$

. . .

- per capita birth rate of juveniles, $\gamma$, bounded above

- 'approximate excess growth rate', $F$, bounded above
    <span class="red">but not necessarily below</span> (logistic growth)

. . . 

Instead of $\Delta$ can have any uniformly elliptic second order differential operator

## Remarks

::: incremental
- Classical models emerge as special cases of the scaling limits
    * Fisher-KPP and Allen-Cahn equations;
        Bolker-Pacala model;
        spatial branching processes
    
- Separation of the two stages of reproduction is still visible
    in the scaling limit: $$\partial_t \eta = r \Delta(\gamma \eta) + F\eta$$

- Using a <span class="blue">lookdown construction</span>, we retain information about genealogies
    in the scaling limit, and hence
    information about population history. <span class="blue">*(Kurtz & Rodrigues 2011, Etheridge & Kurtz 2019)*</span>

:::

# Something about the proof

## Compact containment of $\{\eta^N_\cdot\}_{N \ge 1}$

$$\begin{aligned}
&\langle 1, \eta_t^N(dx)\rangle 
= \langle 1, \eta_0^N(dx)\rangle 
\\ &\qquad {}
+ \int_0^t \big\langle \gamma(x,\eta_s)
    \left(\theta \int \left( r(z, \eta_s) - r(x,\eta_s)\right) q_\theta(x,dz) \right)
\\ &\qquad \qquad {}
+ F(x,\eta_s), \eta_s(dx) \big\rangle ds + M_1^N(t)
\\ &\qquad \qquad \qquad 
\le \langle 1, \eta_0^N\rangle + C \int_0^t \langle 1, \eta_s^N \rangle ds + M_1^N(t) .
\end{aligned}$$

. . .

Grönwall's inequality implies for all $t \in [0,T]$,
$$ \mathbb{E}[\langle 1, \eta_t^N\rangle] \le C_T \mathbb{E}[\langle 1, \eta_0^N\rangle] .$$

. . .

For compact containment, we'd like to bound $\mathbb{E}[\sup_{0\le t\le T}\langle 1, \eta_t^N\rangle]$.

. . .

Taking suprema above, need to control $\sup_{0\le t\le T}M_1^N(t)$.

## A useful trick

$$\begin{aligned}
\langle M_1^N \rangle_t 
&= \frac{\theta}{N} \int_0^t \big\langle \gamma(x,\eta_s) \int r(y,\eta_s) q_\theta(x,dy)
\\ &\qquad {}
+ \left(r(x,\eta_s) \gamma(x,\eta_s) - \frac{1}{\theta}F(x,\eta_s)\right),
\eta_s(x) \big\rangle ds
\end{aligned}$$

::: {.fragment .red}

Problem: $F$ not bounded below.

:::

::: {.fragment .blue}

Solution: Rearrange equation for $\langle 1, \eta_t^N \rangle$
$$\begin{aligned}
&- \int_0^t \langle F(x,\eta_s), \eta_s(dx)\rangle ds 
= \langle 1, \eta_0^N(dx)\rangle - \langle 1, \eta_t^N(dx) \rangle
\\ &\qquad {}
+ \int_0^t \big\langle \gamma(x,\eta_s)
\left( \theta \int (r(z,\eta_s) - r(x,\eta_s)) q_\theta(x,dz) \right),
\eta_s(dx) \big\rangle ds
+ M_1^N(t)
\\ &\qquad\qquad 
\le \langle 1, \eta_0^N \rangle + C \int_0^t \langle 1, \eta_s^N \rangle ds + M_1^N(t)
\end{aligned}$$

:::

-------------

Combining boundedness of $\mathbb{E}[\langle 1, \eta_t^N \rangle]$ and the calculation above,
$\mathbb{E}[\langle M_1^N\rangle_T ] < C'_T$, so

::: incremental

- Burkholder-Davis-Gundy implies $\mathbb{E}[\sup_{0 \le t \le T} M_1^N(t)] < C^{''}_T$

- from which $\mathbb{E}[\sup_{0\le t \le T} \langle 1, \eta_t^N \rangle ] < C^{'''}_T$.

- Markov's inequality then leads to compact containment of $\{\eta^N_\cdot\}_{N \ge 1}$.

:::

# Ancestral lineages

::: blue
Consider a single ancestral lineage
$$L_t = (\text{location of the genetic ancestor time $t$ ago}).$$
:::

. . .

and for this talk, work in the classical PDE limit, so
$$\partial_t \eta = r \Delta(\gamma \eta) + F\eta .$$

---------

![](sims/expansion.pop.mp4)

---------

![](sims/expansion.lineages.mp4)

## Ancestral lineages

Suppose population has a stationary density $w(x)$. Then
$$ dL_t = r(L_t) \gamma(L_t) 2 \nabla \log(w\gamma)(L_t) dt
+ \sqrt{r(L_t)\gamma(L_t)} dB_t$$

. . .

::: incremental
- Lineage speed determined by rate of production of mature offspring ($r\gamma$, $\approx$ death),
- and drawn to regions of high total fecundity ($w \gamma$).
- Reversible with respect to $$\color{red}{\pi(x) = \frac{\gamma(x,w(x)) w(x)^2 }{ r(x,w(x))}.} $$
:::


. . .

<span class="blue">Lineage motion *tells us more* than stationary population density:</span>
$w$ solves
$$ r\Delta(\gamma w) + (r\gamma - \mu) w = 0, $$

. . .

multiply $r$ and $\mu$ by $\lambda$:

- same stationary density, but
- lineages spend more time where $\lambda < 1$: those areas have higher long-term fitness.

# Reaction-diffusion equations and range expansion ($d=1$)

## Fisher-KPP (1937)

$$ \frac{\partial u}{\partial t} = \frac{\partial^2 u}{\partial x^2} + u (1-u) $$

$\gamma \equiv 1$, $r \equiv 1$, $F(x,m) = 1 - m$.

. . .

Traveling wave solution $u(t,x) = w(x - 2t)$,
so lineage moves <span class="red">relative to the wave front</span> as
$$\begin{aligned}
dL_t 
&= 2 \nabla \log(w)(L_t) dt + 2 dt + dB_t
\end{aligned}$$

. . .

$w(x) \sim e^{-x}$, so lineages <span class="blue">stay in the wave front</span>
(where numbers are small and the scaling limit breaks down)


## Allen-Cahn

$$ \frac{\partial u}{\partial t} = \frac{\partial^2 u}{\partial x^2} + u (1-u) \color{blue}{(2u - 1 + s)} 
\qquad \color{blue}{s \in (0, 2)}$$

Now $F(x,m) = (1 - m)(2m-1+s)$, bistable.

. . .

Traveling wave solution $\varphi(t,x) = w(x - st)$
with $w(x) = (1 + e^x)^{-1}$,
so lineage moves <span class="red">relative to the wave front</span> as
$$\begin{aligned}
dL_t 
&= \left(s - 2 \frac{e^{L_t}}{1 + e^{L_t}}\right) dt + dB_t ,
\end{aligned}$$

. . .

with stationary distribution $\propto e^{sx}(1 + e^x)^{-2}$.

. . .

Genealogies known to be Kingman for $s<1$: [Etheridge-Penington 2022](https://projecteuclid.org/journals/electronic-journal-of-probability/volume-27/issue-none/Genealogies-in-bistable-waves/10.1214/22-EJP845.full)


## A less classical example $\hspace{5em}$ <span class="blue">$\gamma \propto$ pop density, logistic control</span>

:::: r-stack

::: {.fragment .coverup}
$$ \frac{\partial u}{\partial t} = \frac{\partial^2}{\partial x^2} (u^2) + u (1-u) ,
\qquad
\phantom{u(t,x) = \left(1 - \exp\left(\frac{1}{2}(x-t)\right)\right)_+}
$$
:::

::: {.fragment .coverup}
$$ \frac{\partial u}{\partial t} = \frac{\partial^2}{\partial x^2} (u^2) + u (1-u) ,
\qquad
\color{red}{u(t,x) = \left(1 - \exp\left(\frac{1}{2}(x-t)\right)\right)_+}
$$
:::

::::

. . .

"Effective" density dependent dispersal -- a <span class="blue">porous medium equation</span>

. . .

::: columns

:::::: {.column width=50%}

![Curves showing wave shape and stationary distribution.](figs/pme_dists.png)

::::::

:::::: {.column width=50%}
:::: incremental
- Ancestral lineage has stationary distribution
$\propto e^x (1 - e^{x/2})$ for $x < 0$
- With noise: genealogies also Kingman?
::::
::::::
:::

---------

![](sims/pme_expansion.lineages.mp4)

# Closing


::: incremental
- PDE/superprocess dichotomy: $\lim \frac{\theta}{N} > 0$
- Nonlinear PDE limits:
    <span class="blue">$$ \partial_t \eta = r \Delta(\gamma \eta) + F \eta . $$</span>
- Lineage motion well-understood in deterministic limit, using a lookdown.
- *Next:* coalescence?
:::

<span class="red fragment">*Remarks:*</span>

::: incremental
- In spite of complexity, some mathematical tractability
- A trace of the two-step reproduction mechanisms persists over large temporal and spatial scales
- Readily simulated in [SLiM](https://messerlab.org/SLiM)
:::


## {data-background-image="figs/guillemots_thanks.png" data-background-position=center data-background-size=50%}

------

![When I was one, lyrics](figs/when_i_was_one.png)

