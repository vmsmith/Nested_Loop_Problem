### Nested Loop Problem

This work is being done on a late-2010 13" MacBook Air running MacOS 10.12.6 (High Sierra). The programming software is R 3.5.0 and RStudio 1.1.442.

#### Background  

I am working on an expected value project where there are five scenarios (A - E): 

![graphic #1](https://github.com/vmsmith/Nested_Loop_Problem/blob/master/graphics/EV1.png)

Each of those five scenarios has an assumed payoff:  

![graphic #2](https://github.com/vmsmith/Nested_Loop_Problem/blob/master/graphics/EV2.png)  

And each of those five scenarios also has a probability that it will occur: 

![graphic #3](https://github.com/vmsmith/Nested_Loop_Problem/blob/master/graphics/EV3.png)  

And of course, the expected value is the sum of the probabilities times their associated payoff:  

![graphic #4](https://github.com/vmsmith/Nested_Loop_Problem/blob/master/graphics/EV4.png)  

#### Approach  

For the time being, I am mainly interested in scenarios A and E and their associated probabilities, α and ε.

I begin by assigning fixed values to α and ε: 

    1: alpha <-  0.70
    2: epsilon <- 0.05

Since α + β + γ + δ + ε = 1, it follows that γ + δ + ε = 1 - (α + β).

I want to let the other probabilities -- β, γ, and δ -- loop through their various combinations.  In this way I actually get a distribution of expected values, and for the time being that is what I want.

So I create a variable that will lay the groundwork for that:

    3: mid_percentages <- 1 - (alpha + epsilon)

With these particular initial values of alpha and epsilon, mid_percentages equals 0.25.

Now I create a vector that will allow me to loop through the various possibilities:

    4: percentages <- seq(0, mid_percentages, .01)

That vector looks like this:

    5: [0.00, 0.01, 0.02, ..., 0.25]

Now I'm ready to begin looping. (And in the spirit of Donald Knuth, I am not optimizing at this point. Later I'll look at the apply family, but not yet.)

Here is my nested loop:

    6: for(beta in percentages){
    7:   for(gamma in percentages){
    8:     for(delta in percentages){
    9:       if(beta + gamma + delta == X){
    10:        do something
    11:       }
    12:     }
    13:   }
    14: }

I am having two problems.

#### Problem #1  

The first problem is that when I replace X (in line 9) with the variable, 

    mid_percentages

I get nothing.

On the other hand, if I replace X with the specific value 0.25, I get something.

And I can see when I run it that 

    mid_percentages == 0.25

So I don't know why the loop works with a specific numeric value but not a variable that equals that specific numeric value.



#### Problem #2  

The second problem -- which I discovered while trying to debug the first -- is that when I loop through, say, 0.25, I don't get the full range of results I expect.

I expect something like this:

    0.00		0.00		0.00
    0.00		0.00		0.01
    0.00		0.00		0.02
    0.00		0.00		0.03

	and so on...

    0.25		0.25		0.22
    0.25		0.25		0.23
    0.25		0.25		0.24
    0.25		0.25		0.25

But I generally get some seemingly random subset of that.  As I increase the size of the variable `alpha`, and the variable `mid_percentages` gets smaller, the output seems to get more pathological.


#### Conclusion  
