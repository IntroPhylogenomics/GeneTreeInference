# Exercise 1 (Sampling)

Let's create our own sample space using the Rev language. We'll begin by creating a vector in RevBayes. There are a few different ways to create a vector, but the simplest is probably to enclose a comma-separated list of values in square brackets [ . . . ]

```
sampleSpace = ["a","b","c"]
```

As with Python, to check the value of any variable, we can simply type the name of that variable and RevBayes will print its current value.

`sampleSpace`

In Rev, we can verify the size of our vector (i.e., the number of values it contains) by using its size() method.

`sampleSpace.size()`

Also like Python, we can check individual values in a vector by using the name of the vector and providing indices. For instance, to look at only the 2nd value in the list we would type

`sampleSpace[2]`

__NOTE that RevBayes (like R) is 1-indexed, while Python is 0-indexed.__

To sample values from our sample space, we need to know a few more things about the Rev language. First, if we want to create a new vector, we can do so implicitly by starting to assign values to individuals positions in the new vector. For instance, if we wanted to store a vector of values (called mySamples) sampled from our sample space, we could start by doing something like this

```
mySamples[1] = "a"
mySamples
```

Rev also contains `for` loops. To indicate a loop over a series of consecutive integers, it uses a convenient notation - the start and end values are just separated with `:`. Code executed as part of the loop is contained inside curly braces { . . .}.

```
for (i in 1:4){
    i
}
```

Now let's set up a for loop to do something more interesting, but we need one more trick. We're going to use a function called `runifInt()`. This name can be broken up into these three parts

1. _r_ (sample values from a distribution)
2. _unif_ (in this case, use a uniform distribution)
3. _Int_ (more specifically, use a uniform distribution across only integers)

A uniform distribution just means that we assign equal probability to all values included in the distribution. `runifInt()` takes three arguments

1. the number of samples you want
2. the lower bound on your uniform distribution
3. the upper bound on your uniform distribution

Using a for loop, we can see what it looks like to sample from this uniform distribution several times.

```
for (i in 1:10){
    runifInt(1,1,5)
}
```



