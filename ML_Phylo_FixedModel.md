# Maximum Likelihood Phylogenetic Inference (Fixed Model)

To start, we will learn how to infer a maximum-likelihood estimate of our phylogeny with a pre-specified model of sequence evolution. With IQTree, this is incredibly easy to do. The program automatically handles the hard work of calculating the likelihoods and finding an efficient algorithm to explore parameter space.

- [IQTree Tutorial on ML Phylogenetic Inference with User-defined Substitution Models](http://www.iqtree.org/doc/Advanced-Tutorial#user-defined-substitution-models)
- [Overview of DNA Models in IQTree](http://www.iqtree.org/doc/Substitution-Models#dna-models)
- [Overview of Models for Rate Heterogeneity Across Sites](http://www.iqtree.org/doc/Substitution-Models#rate-heterogeneity-across-sites)

After looking through these three sections of the IQTree website, try to infer a phylogeny with the concatenated turtles data ([turtle.fa](https://raw.githubusercontent.com/IntroPhylogenomics/GeneTreeInference/master/turtle.fa)) assuming a 

- Jukes-Cantor (JC) model
- JC model with gamma-distributed rate variation (JC+G)
- GTR model
- GTR model with gamma-distributed rate variation (GTR+G)
- GTR model with free rates (GTR+R)

Open the trees you infer (in the `.treefile` files) in FigTree. How do they compare topologically? How do the branch lengths compare?

Now, using the bash skills you learned yesterday, write a script to analyze each gene separately ([download genes here](https://github.com/IntroPhylogenomics/GeneTreeInference/blob/master/turtleGenes.zip)). You may want to have your script start by creating separate folders for each gene and then moving the datasets into their respective folders. See if you can keep this script as short as possible. In other words, avoid just writing out every call to IQTree on its own line. Think about using a loop.
