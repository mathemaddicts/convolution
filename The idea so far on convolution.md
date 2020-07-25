# The idea so far on convolution

I thought it would be a good idea to give an overview of what we've discussed so far on the level of how it provides general strategy for data analysis. See if you guys are on board with this description.


The basic architecture I'm trying to generalize here is this:

![](https://i.imgur.com/pPO4B84.png)

Here are the steps as I see them:

1. Given a data set $D$, find a representation of $D$ as a set of functions $f: X \to \mathbb{R}$ where $X$ is a metric space. 
2. Select a finite set of metric spaces with basepoint $(Y_1,y_1),(Y_2,y_2),...,(Y_n,y_n)$ to serve as "local models" for $X$
3. For each point $x \in X$ and each $i$, find the (or a) "least distortative" map $c_{i,x}:(Y_i,y_i)\to (X,x)$
4. Given a function $f:Y_i\to \mathbb{R}$ and a datapoint $g:X\to\mathbb{R}$ in $D$, we consider the function $\phi(f,g):X\to\mathbb{R}$ given by $\phi_i(f,g)(x)=\sum_{y\in Y_i`} f(y)g(c_{i,x}(y))$. For each choice of $f$ and $i$, we get a feature map in the convolutional layer.
5. Pick a radius $r$ and an $r$-dense subset $X_r$ of $X$. We can pool the data of a feature map by sending $g:X \to \mathbb{R}$ to $g_r: X_r\to\mathbb{R}$ given by sending a point $x$ to the average value of $g$ over the $r$-ball around $x$
6. Flatten the data and analyze via a standard neural network


What do you guys think?

If we align on the framework, then the theoretical tasks are:

1. What are the interesting ways of representing $D$ as functions on a metric space (e.g. using correlation or mutual information?) [Here is a document to discuss this piece.](https://hackmd.io/m2-XCsgQQXyCtPzDdEVt0A)
2. Given $D$ and $X$, what are the interesting ways of finding local models $(Y_i,y_i)$?
3. What's the best way of finding local maps?
4. To what extent is it important to deal with patching together maps?
5. Is pooling something that needs more thought, or can we pretty literally replicate what's done for image convolution?
6. What part of this process should be learned during training, and what parts should be thought of as fixed architecture?


# Thinking Categorically

It seems like there ought to be a way of phrasing what we're up to in terms of something like "replacing the points in a neural network with metric spaces." I'm not sure if this intuition is valid, but it seems like there might be something there.


