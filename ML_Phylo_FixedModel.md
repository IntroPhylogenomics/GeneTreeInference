# Maximum Likelihood Phylogenetic Inference (Fixed Model)

To start, we will learn how to infer a maximum-likelihood estimate of our phylogeny with a pre-specified model of sequence evolution. With IQTree, this is incredibly easy to do. The program automatically handles the hard work of calculating the likelihoods and finding an efficient algorithm to explore parameter space.

- [IQTree Tutorial on ML Phylogenetic Inference with User-defined Substitution Models](http://www.iqtree.org/doc/Advanced-Tutorial#user-defined-substitution-models)
- [Overview of DNA Models in IQTree](http://www.iqtree.org/doc/Substitution-Models#dna-models)
- [Overview of Models for Rate Heterogeneity Across Sites](http://www.iqtree.org/doc/Substitution-Models#rate-heterogeneity-across-sites)

After looking through these three sections of the IQTree website, try to infer a phylogeny with the turtles data assuming a Jukes-Cantor (JC) model, a JC model with gamma-distributed rate variation (JC+G), a GTR model, and a GTR model with gamma-distributed rate variation (GTR+G).
