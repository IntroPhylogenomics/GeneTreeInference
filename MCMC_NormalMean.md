# Inferring the Parameters of a Normal with Markov Chain Monte Carlo (MCMC)

We are interested in learning about the trait values in a population (of salamanders!). We begin by making the assumption that the trait values in our population are normally distributed. We then sample some trait values from the population and try to infer the mean of the overall population based on the sample.

First, we need to define how big our sample size will be.

```
sampleSize <- 10
```

Next, we need to sample this many values from the population. In our case, we will know the true mean (and standard deviation) for our population, because we get to pick them! In RevBayes, functions that draw values from distributions all begin with _r_, because these are functions that draw random values. In our case, we want to draw values from a normal distribution, so we use `rnorm()`.

```
trueMean <- 10                                     # Define mean trait value in the population
trueStandDev <- 1                                  # Define the standard deviation of trait values in the population
data <- rnorm(sampleSize,trueMean,trueStandDev)    # Draw our sample from the population
data                                               # Print our sample to the screen for inspection
```
