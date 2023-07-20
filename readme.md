Contents:

- all latent spaces

- one source, 189 targets

- why not Wasserstein

- triangles and circles

- I want to further simplify this is too tricky


# All latent spaces

Just to let it be known, I have the code to extract all latent spaces and I have indeed extracted all latent spaces from the following experiment. Results following will show the first two (still have to finalize 3rd one, and 4th one is the 1024-dimensional one).

# One source, 189 targets

The source is the dataset with parameters (60,50,195,50)


<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/samples.png?raw=true">


The target is 189 datasets with the parameters specified in the graphs (as usual graphs are WITHOUT, WITH, DIFF from left to right):

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/three_musketeers.png?raw=true">

This is the most stable Wasserstein, implemented in the first and second latent space

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/wasserstein_1.png?raw=true">

<img src="https://github.com/MarcoFurlan99/5_misc_results/blob/master/images/wasserstein_2.png?raw=true">

# Why not Wasserstein

The computational issues with Wasserstein persists, but since last time I was once again told to compute the corresponding graph with the distance measure, well here it is.

