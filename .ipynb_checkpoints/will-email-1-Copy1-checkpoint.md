# A geometric question that came up on Lip(X,X)


Hey guys,

So I've been puzzling over this question of figuring out what the group of near-self isometries is for one of our local neighborhoods, and I realized it's got a much more interesting theoretical component than I realized. I don't think it matters algorithmically, but it's interesting enough that I think we should flag it as something to think about in the future.

The question is this: Given a metric space $X$, what is a good way of thinking of the set of all "near self isometries of $X$"?

1. Bijections of $X$- For a finite metric space $X$, I think what will work for our purposes is to consider the set of bijections from $X$ to $X$. Each such bijection has a Lipschitz constant associated to it, so we just have to label the symmetric group on $X$ with $k$'s. Computationally, starting with k=2 or something, there shouldn't be that many permutations that distort distances by less than a factor of k, so my guess is that computing this will be tractable.

I think this approach will work in practice, but theoretically it seems like it's not quite what we want.

2. Extending $X$ to a larger complex- Another approach that I think Cotton mentioned was to look at some larger space X embeds in and think of near isometries there.  It might be useful to think about convex metric spaces (though I also would be sad to rule out Cantor sets). We can embed any metric space in a convex metric space via the Kuratowski embedding into a Banach space B given by the set of all bounded functions on X with the supremum norm. If i(X) is the image of X in our embedding, we could then think of biLip(B) as being our group of "near self-isometries of X," since any element g of biLip(B) will have the property that g(i(X)) is close to i(X).  This looks like it might actually be computationally tractable– what do you think Cotton?

Ideally, we could compute the set $$\{ g\text{ in biLip(B) } | \text{ distortion}(g)<k\}$$ explicitly, but I don't know if this is just linear algebra or if it's something hard. Also, since we don't have to worry about measures here, we can use any L^p norm instead of the sup norm (though I'm beginning to wonder whether measures should be showing up somehow.)

3.Thinking of X as being sampled from a larger space. This one is still vague to me, but can you guys think of a "manifold learning" type way to think about how to find an enveloping space?

Anyhow, I think this is a super interesting problem. Right now I think the Kuratowski embedding approach looks promising because its completely general and it seems like it's something we can actually compute with. The Kuratowski embeddings for different charts also fit together in a nice way, and it seems like it might even behave well under adding more points in the case where we're sampling from a manifold. There might even be some fun convergence theorems we could prove here. Anyhow, food for thought.

Cheers,

Will

