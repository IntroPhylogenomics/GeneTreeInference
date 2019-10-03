# Maximum Likelihood Inference of the Mean

We are interested in learning about the trait values in a population (of salamanders!). We begin by making the assumption that the trait values in our population are normally distributed. We then sample some trait values from the population and try to infer the mean of the overall population based on the sample.

First, we need to define how big our sample size will be.

`sampleSize <- 10`

Next, we need to sample this many values from the population. In our case, we will know the true mean (and standard deviation) for our population, because we get to pick them! In RevBayes, functions that draw values from distributions all begin with __r__, because these are functions that draw random values. In our case, we want to draw values from a normal distribution, so we use `rnorm()`.

```
trueMean <- 10                                     # Define mean trait value in the population
trueStandDev <- 1                                  # Define the standard deviation of trait values in the population
data <- rnorm(sampleSize,trueMean,trueStandDev)    # Draw our sample from the population
data                                               # Print our sample to the screen for inspection
```

Now that we have some data, we need to be able to calculate the likelihood, P(_D_|_H_). In this case, our hypothesis (_H_) is a Normal distribution with a given mean and standard deviation. _D_ represents the data, the values sampled from our "true" Normal distribution. To do this, we'll create our own function.

```
# This function loops over values in our dataset and returns the log-likelihood of the data.
# clear(calcLike) # Use this to remove previous function definition if defining again.
function calcLike (Real[] dat, Real mean, Real stdev){
    logLike <- 0.0
    for (d in dat){
        logLike += dnorm(d,mean,stdev)
    }
    return logLike
}
```

We also need to give these variables starting values, to define a starting place for our exploration of parameter space. To do so, we'll draw random values.

```
m <- rUniform(1,0,50)  # Draw 1 value from a Uniform(0,50) distribution
sd <- rUniform(1,0,4)  # Draw 1 value from a Uniform(0,4) distribution
```

Let's print these values, just to see where we'll be starting.

```
m[1]  # Even though m has just one value, it's stored in a vector so we need to extract it
sd[1] # The same for the standard deviation
```

Let's calculate the likelihood for the starting values of our mean and standard deviation.

```
likes <- [calcLike(data,m[1],sd[1])]
likes[1]
```
