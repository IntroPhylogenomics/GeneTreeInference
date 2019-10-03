# Maximum Likelihood Estimation of a Genetic Distance

We're going to walk through the steps of estimating the maximum likelihood genetic distance between two sequences under the Jukes-Cantor model of sequence evolution. In the case of Jukes-Cantor, the probability of change (or no change) given a distance (_t_, in expected number of changes per site) has an analytical derivation (see Yang, Chapter 1). As with most phylogenetic analyses, we will be taking advantage of the assumption that each site evolves independently.

```
clear()

# Calculates the probability that one site does NOT change

function probStaySame(Real t){
    if (t >= 0.0){
        pZero = (1/4) + ((3/4)*exp(-4*(t/3)))
        return abs(pZero)
    } else {
        return abs(0.0)
    }
}


# Calculates the probability that a site DOES change

function probChange(Real t){
    if (t >= 0.0){
        pOne = (1/4) - ((1/4)*exp(-4*(t/3)))
        return abs(pOne)
    } else {
        return abs(0.0)
    }
}
```

Now we can use these individual probabilities to fill out an entire transition matrix for distance _t_. We won't actually use the full matrix for these calculations (since we have expressions for each probability independently), but we would need to use the matrix for more complicated models.

```
# Returns the entire transition probability matrix for a given branch length
# Jukes-Cantor model

function jcTranMatrix(Real t){
    return [[probStaySame(t),probChange(t),probChange(t),probChange(t)],
           [probChange(t),probStaySame(t),probChange(t),probChange(t)],
           [probChange(t),probChange(t),probStaySame(t),probChange(t)],
           [probChange(t),probChange(t),probChange(t),probStaySame(t)]]
}
```

Now we need to define a function to calculate the likelihood for a given genetic distance and two sequences (as strings).

```
# Returns the likelihood for distance t given two sequences
# Jukes-Cantor model
# Requires probStaySame() and probChange()

function distLike(String seqOne, String seqTwo, Real t){
    logLike = 0.0
    numSites = seqOne.size()
    for (i in 1:numSites){
        isSame = (seqOne[i] == seqTwo[i])
        if (isSame){
            logLike += ln(probStaySame(t))
        } else {
            logLike += ln(probChange(t))
        }
    }
    return logLike
}
```

The function `distLike()`, given above, takes two strings representing DNA sequences and a _t_ as input. Copy this function into a text editor and turn it into pseudocode. How does the function work? How are we using the assumption of site independence?

Now we can use exactly the same hill climbing algorithm that we used to find the maximum likelihood estimate (MLE) for the mean of the Normal distribution. The only difference here is that we've substituted our new likelihood function.

```
# A hill-climbing algorithm to find the maximum likelihood distance t given two sequences
# Jukes-Cantor
# Requires distLike()

function distML(String seqOne, String seqTwo, Real t, Real stepSize){
    like = distLike(seqOne,seqTwo,t)
    while (distLike(seqOne,seqTwo,t+stepSize) > like){
        t = t + stepSize
        like = distLike(seqOne,seqTwo,t)
    }
    while (distLike(seqOne,seqTwo,t-stepSize) > like){
        t = t - stepSize
        like = distLike(seqOne,seqTwo,t)
    }
    if(stepSize > 0.0001){
        t = distML(seq1,seq2,t,stepSize/2.0)
    }
    return t
}
```

The function above is a hill-climbing algorithm to attempt to find the MLE of genetic distance between two sequences (given as strings or lists). The arguments to the function include:

- The first sequence
- The second sequence
- A starting value for genetic distance, _t_.
- The initial step size used to explore different values of _t_.

```
# Defining sequences to calculate distance between

seq1 = "AAGTCCAG"
seq2 = "AAGCCCCG"
```

Now that we've defined our sequences, let's explore the relationship between different potential genetic distances and likelihood. First, we'll loop through a set of distances between 0.05 and 1 and calculate the associated likelihoods.

```
# Calculate likelihoods for different distances (0.05-1.0)

for (t in seq(from=0.05,to=1.0,by=0.05)){
    distLike(seq1,seq2,t)
}
```

What do these values look like? What kinds of numbers are these? Roughly where do you think the MLE is? How confident can we be in this MLE?

```
# Now we'll use the hill-climbing function to estimate the MLE

distML(seq1,seq2,0.05,0.1)
```
