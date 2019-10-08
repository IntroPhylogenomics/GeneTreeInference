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

Now that we have some data, we need to assign prior probability distributions to our model parameters and figure out how to calculate the likelihood. For our purposes, we will make the assumption that our true mean has uniform probability of being between 0 and 50, while the standard deviation has a uniform probability of being between 0 and 4. In this toy case, we will not specify how we came to these decisions, but for analyses of empirical data we would need to use outside information to set reasonable limits on the range of possible values for these parameters.

```
# Mean has a Uniform(0,50) prior
# Standard deviation has a Uniform (0,4) prior
```

We also need to give these variables starting values, to define a starting place for our exploration of parameter space. To do so, we'll draw random values from their prior distributions.

```
m <- rUniform(1,0,50)  # Draw 1 value from a Uniform(0,50) distribution
sd <- rUniform(1,0,4)  # Draw 1 value from a Uniform(0,4) distribution
```

Let's print these values, just to see where we'll be starting.

```
data
m[1]  # Even though m has just one value, it's stored in a vector so we need to extract it
sd[1] # The same for the standard deviation
```

Now we need a way to calculate the likelihood, _P_(_D_|_H_). In this case, our hypothesis (_H_) is a Normal distribution with a given mean and standard deviation. _D_ represents the data, the values sampled from our "true" Normal distribution. To do this, we'll create our own function.

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

Let's calculate the likelihood for the starting values of our mean and standard deviation.

```
likes <- [calcLike(data,m[1],sd[1])]
likes[1]
```

Now we'll begin sampling using the Metropolis-Hastings algorithm. For the proposal distribution of our sampler, we'll use a Normal distribution. Remember, this Normal is not related to the distribution of trait values in the population, it is simply a function that gives us a way to propose moves through parameter space.

Recall that the general outline of each Metropolis-Hastings step is:

- Propose a new set of parameter values
- Compare the posterior density of the proposed position to the current position
- Decide whether to accept the proposal based on the comparison
- Add the chosen values to the chain

As an exercise, add your own pseudocode to label the steps in the Metropolis-Hastings algorithm below.

```
numGens = 3000
for (gen in 1:numGens){
    
    if (gen % 500 == 0){
        print(gen)
    }
    
    currLike <- calcLike(data,m[gen],sd[gen])
    
    propMean <- rnorm(1,m[gen],1)
    propSD <- rnorm(1,sd[gen],1)
    propLike <- calcLike(data,propMean[1],propSD[1])
    
    LR <- (propLike-currLike)
    
    priorR <- (1/50)
    if (propSD[1] < 0) { priorR <- 0.0 }
    if (propSD[1] > 4) { priorR <- 0.0 }
    if (propMean[1] < 0) { priorR <- 0.0 }
    if (propMean[1] > 50) { priorR <- 0.0 }
    
    ranNumber <- runif(1,0,1)
    
    if (exp(LR)*priorR > 1){
        likes.append(propLike)
        m.append(propMean)
        sd.append(propSD)
    } else if (exp(LR)*priorR > ranNumber[1]){
        likes.append(propLike)
        m.append(propMean)
        sd.append(propSD)
    } else {
        likes.append(currLike)
        m.append(m[gen])
        sd.append(sd[gen])
    }
    
}

burnin = 1000

posteriorMean = 0.0
for (i in burnin:numGens){
    posteriorMean += m[i]
}
posteriorMean = posteriorMean/(numGens-burnin)
posteriorMean

posteriorSD = 0.0
for (i in burnin:numGens){
    posteriorSD += sd[i]
}
posteriorSD = posteriorSD/(numGens-burnin)
posteriorSD
```

Let's take a look at the values we've sampled, and their likelihoods. We could also visualize trace plots for these parameters in R or Python.

```
m
sd
likes
```

Explore the behavior of the sampler as you change:

- The size of the proposal distributions
- The number of generations
- The amount of burn-in

While the starting parameter values are chosen at random, how does the behavior of the chain vary with different starting values?

```
# Use as needed to clear your RevBayes workspace and start again
clear()
```
