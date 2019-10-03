# Discrete Markov Chain Simulation

In this exercise, we are going to explore some properties of discrete-time Markov chains. To do this, we'll define a custom state space and transition matrix, which contains the pairwise probabilities of transitioning between states. By default, our state space consists of two types of days - `Rainy` and `Sunny`. In the Rev language, we encode our states in a one-dimensional vector that we are calling `stateSpace`. We encode our transition matrix as a two-dimensional vector - a vector of vectors - called `transitionMatrix`. We also create a vector to hold the states of our chain, `myChain`, and provide one initial state (in this case, `Rainy`).

```
# Clear our workspace to start
clear()

# Define the states for our chain
stateSpace = ["Rainy","Sunny"]

# Define our transition matrix
transitionMatrix = [[0.8,0.2],[0.2,0.]]

# Initialize our chain
myChain = ["Rainy"]
```

Now that we've initialized our chain, we need a way to draw a new state for each generation. Since this is something we'll want to do a lot, we'll create a new function called `addState`.

```
function addState(String[] chain, String[] states, Probability[][] tMat){

    numStates = states.size()
    
    for (s in 1:numStates){
        if (chain[chain.size()] == states[s]){
            probs = tMat[s]
        }
    }
    
    ranNum = runif(1,0,1)[1]
    
    probSum = 0.0
    
    i = 1
    while(probSum < ranNum){
        probSum += probs[i]
        if (ranNum < probSum){
            return append(chain,states[i])
        }
        i += 1
    }     
}
```
