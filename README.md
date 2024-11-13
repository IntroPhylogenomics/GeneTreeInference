# Inferring Gene Trees

This repository contains tutorials for learning about maximum likelihood (ML) and Bayesian inference of trees from individual genes. For ML inference, we will use [IQTree](http://www.iqtree.org). For Bayesian inference, we will use [RevBayes](https://revbayes.github.io). [AliView](http://www.ormbunkar.se/aliview/) will also be helpful to view sequence alignments, and [FigTree](http://tree.bio.ed.ac.uk/software/figtree/) will be helpful to view trees. Finally, a software tool called (Tracer)[https://github.com/beast-dev/tracer/releases/tag/v1.7.2] is useful for diagnosing the performance of our MCMC based analyses.

- Maximum likelihood inference (general)
  - [Genetic Distance](https://github.com/IntroPhylogenomics/GeneTreeInference/blob/master/ML_GeneticDistance.md)
- Maximum likelihood inference (phylogenies)
  - [Fixed Model of Sequence Evolution](https://github.com/IntroPhylogenomics/GeneTreeInference/blob/master/ML_Phylo_FixedModel.md)
- Nonparametric bootstrapping
  - [Phylogenetic Bootstrapping](https://github.com/IntroPhylogenomics/GeneTreeInference/blob/master/PhyloBootstrap.md)
- Bayesian inference with Markov chain Monte Carlo (general)
  - [Mean of a Normal](https://github.com/IntroPhylogenomics/GeneTreeInference/blob/master/MCMC_NormalMean.md)
  - [Introduction to Graphical Models](https://github.com/IntroPhylogenomics/GeneTreeInference/blob/master/IntroToGraphicalModels.md)
- Bayesian inference with MCMC (phylogenies)
  - [Phylogenetic MCMC with a Fixed Model](https://revbayes.github.io/tutorials/ctmc/)
  - [Debugging your Markov chain Monte Carlo (MCMC)](https://revbayes.github.io/tutorials/mcmc_troubleshooting/) and a [related paper](https://open-research-europe.ec.europa.eu/articles/3-204). Using [RWTY](https://cran.r-project.org/web/packages/rwty/vignettes/rwty.html), to assess convergence and mixing for topologies.
