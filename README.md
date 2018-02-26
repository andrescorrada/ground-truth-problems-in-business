# ground-truth-problems-in-business
Collection of papers and presentations related to ground truth inference in data science

The Flammarion engraving is frequently taken as a metaphor for piercing the veil of reality to understand what is really going on. The engraving also illustrates the goal of solving *ground truth problems* in business. In your company the ground truth of the production data stream may not be known. Or it be hard to compute. Or private.

This collection contains examples of my work that solve the ground truth inference problem by estimating a statistic of ground truth without knowing ground truth itself.

The term *ground truth* sounds fancy and philosophical but it is not. It actually is easy to understand and it is just a generic term for the different forms it takes. Let's take one case I discuss here - binary classification. You have a bunch of data and each of your data points has an "A" or "B" label. The ground truth for that data would be the list
<a href="https://www.codecogs.com/eqnedit.php?latex=\{\ell_{i,\text{true}}\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\{\ell_{i,\text{true}}\}" title="\{\ell_{i,\text{true}}\}" /></a>

