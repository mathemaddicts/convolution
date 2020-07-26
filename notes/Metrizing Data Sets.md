# 1. Metrizing Data Sets

Suppose we are given a data set $X$. What are the interesting / insightful ways of representing $X$ as functions on a metric space?

$$ e = mc^2 $$

$$ e=mc^2 $$
$$ e=mc^2 \tag{} $$

\begin{equation}
E = F \cdot s 
\end{equation}

## 1.A. Representing a data set as a function space

There seem to be a few standard data-structures that might be relevant here.

### Case 1: 

Our data is given as a finite set $S$ of points in $\mathbb{R}^n$.

This seems to be the typical setting we're in, though we can generalized this by:


### Case 2: 

Our data is given as a finite collection $F$ of functions from a set $Y$ to $\mathbb{R}^n$.

Note that Case 2 generalizes Case 1 in two different ways. One is by letting $Y=\{pt\}$ and considering the points in $S$ as maps from $Y\to \mathbb{R}^n$, the other is by letting $Y=\{y_1,y_2,\dots,y_n\}$ and associating each point $(a_1,\dots, a_n)$ in $S$ with the function $f$ with $f(y_i)=a_i$. We've usually been talking about the latter.

Manifold learning also seems to offer some interesting ways of generalizing the $Y=\{pt\}$ case. Suppose the data set $S$ in $\mathbb{R}^n$ is "well approximated" by a submanifold $Y$ of $\mathbb{R}^n$ in the sens that $S$ lies in a tubular neighborhood of $Y$. Then we can represent $X$ in terms of fuctions $f:Y \to \mathbb{R}^{n-m}$ via the normal exponential map.

Case 2 seems to be how, say the data for recommender systems is given, since in that context a person is thought of as, say, a function from movies to how they rate them along various dimensions. 

### Additional cases?
Are there other natural ways a dataset can be given that we should keep in mind here? It would be interesting to consider situations that don't lend themselves to a functional description as well as those that do.

## A dual viewpoint on 1.A

Another way of thinking of representing a data set $X\subset \mathbb{R}^n$ as a set of functions $f:Y \to \mathbb{R}^m$ is as follows. Let $\Phi:X\to (\mathbb{R}^m)^Y$ be an injection. 

Then each point in $Y$ give rise to functions $X\to \mathbb{R}^m$ via the map $x\mapsto \Phi(x)(y)$. So we can think of $Y$ as a set of functions on $X$. This seems natural when $Y$ is, say, coordinate functions on $\mathbb{R}^n$.

Going the other way, suppose we have a set $Y$ of functions from $X \to \mathbb{R^m}$. By the same logic, each point $x\in X$ gives rise to a function $Y\to\mathbb{R}^m$ via the map $y \mapsto y(x)$.

So this means that the class of representations of a dataset $X$ as a function space is the same as the class of functions on $X$. This seems much more general than the discussion above.

It also suggests an interesting strategy to look for representations as function spaces, which is just to take a random collection functions on $X$ as a starting point. This might make sense if, say, the coordinates on $X$ have no natural meaning.

## 1.B. Metrizing a function space

After going through step 1.A, we now have a representation of our data set as a collection of functions $X=\{f_i: Y\to\mathbb{R}^n\}$. We now want to use this to create a metric on $Y$.

### 1.B.1 Metrization using $L^p$ spaces

The first type of metric is the following:

$d(y_1,y_2)=\left(\sum_i |f_i(y_1)-f_i(y_2)|^p \right)^{1/p}$

It's a little weird that what's going on here isn't that we think of $L^p(Y)$, but rather we consider points of $Y$ as functionals on the data points via the map $f_i \mapsto f_i(y)$.

This becomes much more natural when we think of $Y$ as functions on $X$, in which case we can write it as 

$d(y_1,y_2)=\left(\sum_{x\in X} \|y_1(x))-y_2(x))\|^p \right)^{1/p}$,

i.e. it's the familiar $L^p$ distance on $Y$ considered as a subset of $(\mathbb{R}^m)^X$.

### 1.B.2 Metrization using correlation

Similar to $L^p$, we can consider the (pseudo)-metric given by correlation between points in $y$ given as functions on $X$, i.e.

$d(y_1,y_2)=\arccos(cor(y_1,y_2))$

where

$cor(y_1,y_2)= \frac{\sum_{x\in X} y_1(x)\cdot y_2(x)}{\|y_1\|\|y_2\|}$

and $\|y_i\|= \sqrt{\sum_{x\in X} y_1(x)\cdot y_1(x)}$.


### 1.B.3 Metrization using entropy / mutual information

For this, we will consider the set $Y$ as functions from $X$ to $\mathbb{R}^n$. To each $y$ in $Y$, we associate a probability mass function on $X$ given by 

$m_y(x) = \frac{y(x)\cdot y(x)}{\sum_{x\in X}y(x)\cdot y(x)}$

We then set

$d(y_1,y_2)= H(y_1|y_2)+H(y_2|y_1)$, where $H$ is the conditional entropy function

$H(A|B)= \sum_{ a \in sup(A) , b \in sup(B) } A(a)B(b) \log\left(\frac{B(b)}{A(a)B(b)}\right)$

This one seems the most interesting, in part because it breaks up into the two functions $H(y_1|y_2)$ and $H(y_2|y_1)$, both of which are quasi-metrics since they independently satisfy the triangle inequality.

The vanishing of these quasi-metrics has an interesting interpretation. [$H(y_2|y_1)=0$ means that $y_2$ can be written as $f\circ y_1$ for some function $f$.](https://math.stackexchange.com/questions/1404725/zero-conditional-entropy)

One reason why this might be interesting in a neural network setting is that if you pick a bunch of "random" functions on a space $X$ to start out for finding a metric, then you might be curious to know which of these functions are redundant. If you find $y_i$ and $y_j$ such that $H(m_{y_i}|m_{y_j})$ is small, then $y_j$ is "almost" a function of $y_i$ and you might be able to throw it out of consideration.

### 1.B.5 "Transport style" metrics

Supposing that we've already defined one metric, $d$, on our space $Y$ (via one of the above constructions for example). For any set $K \subset \text{Aut}(Y)$ of automorphisms of $Y$, we can define a new metric

$$ d_K(y,y') = \min_{h\in K} d(h(y), y') $$

I think of these as related to "Wasserstein-like" distances, but it's a very general and maybe useful construction I think. A relevant example would be to define a distance between probability distributions on a fixed space, which would measure their similarity in "shape," but not location.

<!-- As described in 1.B.1, these metrics are easiest described if we take the dual perspective, viewing $Y$ as a set of functions on $X$, in which case we're trying to metrize the function space $Y$. An interesting and v -->


### Q: What are the other interesting ways of putting a (quasi)-metric on a function space? 


## Notes / Questions

### 1. Can we use generalized functions?

Should we be committed to the idea of representing data as a collection of functions? Can we do this in the more general setting where we only have relations $r_i \subset Y\times \mathbb{R}^n$ or measures $m_i$ on $Y\times \mathbb{R}^n$ thought of as correlations?

### 2. Can we use generalized metric spaces?

Is a metric space the right level of generality, or is a quasi-metric space sufficient

### 3. What's the most general thing we