# Introduction to Graphical Models

The first, and simplest, type of node in a graphical model is a constant node. These behave essentially just like standard variables in any programming language, and take fixed values. This is also the only type of node that does not depend on the value of any other node in the graph (it is independent of all other nodes).

```
# x is a constant node with a fixed value
x <- 2.3
```

The next type of node is a deterministic node. The values of deterministic nodes do depend on the values of other nodes, but in a completely deterministic fashion. For instance, a simple deterministic node, y, could always have a value that is twice that of x.

```
# Printing the starting value of x
print("x = " + x)

# Defining y using the syntax for a deterministic node
y := 2 * x
print("y = " + y)

# Updating the value of x, but printing the new value of y
# Notice that y itself was never directly changed!
x <- 4.7
print("y = " + y)
```

Notice how the value of y changes as x changes, without having to make a new assignment to y. More complicated deterministic relationships could depend on the values of two or more other nodes.

```
# A more complicated deterministic relationship
k <- 3
m <- 2
n := k^m
print("n = " + n)
```

The third, and final, type of node in a graphical model is a stochastic node. These nodes represent random variables, whose distribution must be specified when the node is created. The parameters of the stochastic node's distribution can either be fixed or can be determined by other variables (nodes) in the model.

```
# Specifying the probability of success for a Bernoulli with a constant node
p <- 0.5

# Creating a new stochastic node to represent the outcome of a Bernoulli trial
z ~ dnBernoulli(p)
print("z = " + z)
```

Note that each time you assign a distribution to a stochastic node, it draws a new value of the random variable.

```
for (i in 1:10){
    z ~ dnBernoulli(p)
    print("z = " + z)
}
```

> _Practice Exercise_
>
> In the code block below, repeat what we did above for the Bernoulli distribution, but this time construct a stochastic node whose values are binomially distributed. Remember that the binomial distribution requires two parameters. If you need some help, you can consult the list of RevBayes commands and distributions.
> 
> `# Write Rev code to define a binomial distribution and draw 10 values from it.`
>
> `# YOUR CODE HERE`
> `# YOUR CODE HERE`

