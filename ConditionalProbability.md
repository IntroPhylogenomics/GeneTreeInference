# Conditional Probability

Even with 1,000 samples, our estimates still have some error, but let's take them as true for the moment. The estimates I obtained were 0.371, 0.179, 0.181, and 0.269. Because our four phenotypes are combinations of two binary traits (large v small, striped v spotted), we can ask whether the states of these characters are independent of one another or not.

A basic axiom of probability is that if two characters are independent of one another, their joint probability can be obtained by multiplying their individual probabilities. In our case, we can examine the independence of large and striped. To find the overall probability of the event large, we need to add the probabilities of "large_striped" and "large_spotted".

```
phenoFreqs = [0.371,0.179,0.181,0.269]

pLarge = phenoFreqs[1] + phenoFreqs[3]
pLarge
```

We can obtain the overall probability of striped by adding the probabilities of "large_striped" and "small_striped".

```
pStriped = phenoFreqs[1] + phenoFreqs[2]
pStriped
```

If these states are independent, then the joint probability of the two conditions together should be given by

```
pLargeStriped_ind = pLarge * pStriped
pLargeStriped_ind
```

How does this value compare to the frequency that was actually observed for that combination? Do you think these traits are independent?

Let's do similar calculations for the other traits.

```
pSmall = phenoFreqs[2] + phenoFreqs[4]
pSmall

pSpotted = phenoFreqs[3] + phenoFreqs[4]
pSpotted

pSmallStriped_ind = pSmall * pStriped
pSmallStriped_ind

pLargeSpotted_ind = pLarge * pSpotted
pLargeSpotted_ind

pSmallSpotted_ind = pSmall * pSpotted
pSmallSpotted_ind
```

Now, comparing all four of these expected phenotype frequencies to those estimated from sampling above, what do you notice? If there are differences, what do they suggest about the (in)dependence of the two traits in this population?

We can also calculate the joint probability of two events without assuming that they are independent. To do so, we use conditional probabilities.

To do these calculations, we'll need to calculate a couple of new values. These are the conditional probabilities.

These can be read as "the probability of being large, given that an individual is striped" or "the probability of being striped, given that an individual is large". To calculate P(large|striped) we can take the frequency of large, striped individuals that we've sampled and divide it by the total frequency of all striped individuals.

```
pLargeGivenStriped = phenoFreqs[1]/pStriped
pLargeGivenStriped
```

Conditional probabilites are very important for Bayesian inference, which we'll talk about soon.
