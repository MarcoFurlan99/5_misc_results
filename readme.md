Contents:

- all latent spaces

- one source, 189 targets

- why not Wasserstein

- triangles and circles

- I'm in need of something simpler

# All latent spaces

Just to let it be known, I have the code to extract all latent spaces and I have indeed extracted all latent spaces from the following experiment. Results following will show the first two (still have to finalize 3rd one, and 4th one is the 1024-dimensional one).

# One source, 189 targets

The source is the dataset with parameters (60,50,195,50)


<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/samples.png?raw=true">


The target is 189 datasets with the parameters specified in the graphs (as usual graphs are WITHOUT, WITH, DIFF from left to right):

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/three_musketeers.png?raw=true">

It has plenty of interesting facts and it essentially allows to get any conclusion we want about the relationship between noise parameters and BN adaptation improvement. So if we are asking ourself "what happens when $\sigma_1$ is constant but $\sigma_2$ varies?" this graph has the answer. Generally it makes sense (top left is easiest, bottom right is hardest, per-graph it's hardest to easiest from left to right). I could write down all my observations as usual but honestly I leave you the data and let you draw your own conclusions about it, then we can discuss them together.

This is the most stable Wasserstein I could create, implemented in the first and second latent space (some values are excluded because not relevant, and I should've excluded more honestly):

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/wasserstein_1.png?raw=true">

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/wasserstein_2.png?raw=true">

I don't have anything to say about the relationship between Wasserstein and the BN adaptation performance, I'm not a big Wasserstein believer at the moment.

# Why not Wasserstein

The computational issues with Wasserstein persists, but since I was once again told to compute the corresponding graph with the distance measure, well I did and it's working the other way around (bigger values in diff graph <-> smaller values in IoU generally). So I'd just let go of the idea of the Wasserstein for the following reasons:

- If it's predicting anything, it is the other way around;

- The calculated square root matrices required in the W's calculations should be symmetric positive semidefinite but I verified that often they are not;

- I'm not sure if the computations are returning the Wasserstein distance in a 1024-dimensional case, a lot of previous tries showed instability in the output and I have no guarantee that this final version, despite being the most stable yet, is returning the actual Wasserstein, except from smaller sized examples (how would I even test if it is in 1024 dimensions??);

- the results that Alex and Luc got all involve the target-normalized Wasserstein distance. I tried implementing it but it requires computing inverse matrices and inverse square root matrices which cause even more issues computationally, consequently the final result was barely stable and probably far from the real value (if I multiplied the input by k the distance should increase by k but instead returned arbitrary-looking values and often negative ones as well);

I was told to use the [Fréchet inception distance](https://en.wikipedia.org/wiki/Fr%C3%A9chet_inception_distance), but it's literally the formula of the Wasserstein distance used for any distribution (without the normality assumption). So it's essentially what we've called Wasserstein distance so far.

# Triangles and circles

Here is the triangles and circles dataset:

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/source.png?raw=true">

We want to identify the <u>triangles</u>.

Here are the results:

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/three_musketeers_toc.png?raw=true">

The parameters are intentionally the same ones as an old experiment of mine with the usual dataset. For comparison:

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/samples_2.png?raw=true">

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/three_musketeers_2.png?raw=true">

# I'm in need of something simpler

I want to do some testing where I don't take the last layer of a UNet which is 1024-dimensional and try to compute a Wasserstein distance off of it. It feels like doing the first driving lessons on a 10 tons truck. I am thinking of taking it down a notch: I want to build a very simple CNN with a single BN layer, getting some understanding and clear results, and then building from there more complex models, making my way up slowly but surely until I get to results which apply in general, and finally testing them on the UNet.

Moreover, Luc's experiment from the paper calculates the Wasserstein off of the normal distributions themselves which generate the dataset, so I want to also do more testing on that and see how far I can go. It should be relatively easy and take little time.

I'd love discussing about what would be a good path to follow.
