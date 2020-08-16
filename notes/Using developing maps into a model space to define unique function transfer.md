# Using developing maps into a model space to define unique function transfer

[![hackmd-github-sync-badge](https://hackmd.io/ISMkM6iITluANUxqN3aGGw/badge)](https://hackmd.io/ISMkM6iITluANUxqN3aGGw)

### A framework for transferring functions

Here is a not very general model for function transfer from one chart to another.

Let $X$ be a metric space, $Y$ be a space on which $G$ acts transitively and freely that we use as a chart space.

Let $U_1$ and $U_2$ be local neighborhoods of $X$ that admit charts valued in $Y$.

We are looking for maps $Z^{U_1}\to Z^{U_2}$ for arbitrary $Z$.

Step 1. Pick a chart $\phi_1:U_1\to Y$.
Step 2. Find an extension $Z^{\phi_1(U_1)}\to Z^Y$
Step 3. Find a correspondence between charts from $U_1\to Y$ to charts $U_2\to Y$ (use a developing map)
Step 4. Find an element of $G$ that minimizes the Gromov-Hausdorff distance between $U_1$ and $g\cdot U_2$

If $Y$ is an arbitrary space, we have $Stab(y)$ for $y\in Y$. 

$\mathbb{R}^2\hookrightarrow Isom(\mathbb{R}^2)\to S^1$

$G = \text{Isom}(\mathbf{R}^2) = \rtimes$ acting on $\mathbf{R}^2$ by isometries. $\text{Fix}(x \in \mathbf{R}^2)$ is a copy of $SO(3)$, and $G

$\mathbb{R}^2\hookrightarrow Isom(\mathbb{R}^2)\to S^1$


### An Example to Illustrate This

Let $X$ be a finite set, metrized by pulling back the metric on $\mathbb{R}^2$ via an embedding of $X$ into $\mathbb{R}^2$. 

**Note 1:** I could have just said let $X$ be a finite set of points in $\mathbb{R}^2$, but the ambient space is extrinsic information that we don't need. 

**Note 2:** A specific example to have in mind here is that $X$ is a grid of pixels, metrized via pixel coordinates so that the distance between the $(i,j)$-pixel and the $(k,l)$-pixel is $((i-k)^2+(j-l)^2)^{\frac{1}{2}}$.


Here's an image of such an $X$:

![](https://i.imgur.com/jBpAmqq.png =300x300)

Now suppose that we have two different R-balls in $X$ $B_1$ and $B_2$:

![](https://i.imgur.com/qZD3UPx.png =300x300)


Let's suppose also that we have a function $f:B_1\to \mathbb{R}$. 

Here's a blown up visualization:

![](https://i.imgur.com/ytKlfjM.png =300x300)


We'd now like to ask, what is the "same function" at $B_2$?

The basic strategy is to try to "match up" as best as possible the image of $B_2$ under a chart to $\mathbb{R}^2$ with the image of $B_1$.

Here's an image of $B_2$ quite close to $B_1$:

![](https://i.imgur.com/r9e49A2.png =300x300)

We can then imagine "coloring" the points of $B_2$ to match as close as possible the colors of $B_1$.

The issue here is that there are a lot of reasonably good matchings between $B_1$ and $B_2$. For example, leaving $B_1$ fixed and rotating $B_2$ by 45 degrees we get:

![](https://i.imgur.com/IvhGfxo.png =300x300)

So we should expect ambiguity in this transfer function up to rotation.

We'd like to get rid of this ambiguity, which is where developing maps come in.

To start out with, we choose a path between $B_1$ and $B_2$, which defines a chain of overlapping charts. In our case, we just need one more chart $B_3$:

![](https://i.imgur.com/eca5Ffk.png =300x300)

We'd now like to find a "developing map" that chains charts together in $Y$.

We start with a chosen chart for $\phi:B_1\to\mathbb{R}^2$:

![](https://i.imgur.com/62Dn2SG.png =300x300)

We then look for a chart $\psi: B_3\to \mathbb{R}^2$ such that $\phi|_{B_1\cap B_3} = \psi|_{B_1\cap B_3}$:

![](https://i.imgur.com/QqIZPW6.png =300x300)


And finally a chart $\theta: B_2\to \mathbb{R}^2$ such that $\theta|_{B_2\cap B_3} = \psi|_{B_2\cap B_3}$:

![](https://i.imgur.com/87HcLNM.png =300x300)

The upshot here is that we've now got a specific chart $\theta$ "corresponding" to the initial chart $\phi$. We can think of this if we like an "extension" $\tilde{\phi}$ of $\phi$ to the union $B_1\cup B_2$:


![](https://i.imgur.com/gKg8jpK.png =300x300)

This extension can in general depend on the path between $B_1$ and $B_2$, but should be "topological" if maps extend uniquely (as they do in this case.)

How does this help? Well we can now use our translation group $H$ (which acts freely and transitively on the plane) to get a *unique* correspondence (at least once we choose a base point) between the balls via an element $h\in H$.

![](https://i.imgur.com/89YRixw.png =300x300)

It's this uniqueness of the correspondence that will allow us to do standard edge detection.

So applying this method we now get a preferred matching between $B_1$ and $B_2$ (or at the very least we've removed the ambiguity of rotations):

![](https://i.imgur.com/r9e49A2.png =300x300)

## Transferring functions

There's now a question of how to actually "pick up" the colors from $B_1$ and transfer them to $B_2$, i.e. how we extend the function from the image of $B_1$ in $Y$ to the union of the images of $B_1$ and $B_2$.

When the target of the charts is a linear space, we can do some sort of averaging. In general however, it seems to be elegant to try to extend the functions from $B_1$ to all of $Y$ (in this case $\mathbb{R}^2$). This allows us to "color" arbitrary charts to $Y$ in a uniform way.

In the example chosen, we can imagine an extension to the plane:
![](https://i.imgur.com/ytKlfjM.png =200x200)![](https://i.imgur.com/ksfNnYh.png =200x200)

We can then define map on the union of the images $B_1$ and $B_2$ by restriction:

![](https://i.imgur.com/1b66TeF.png =200x200)


