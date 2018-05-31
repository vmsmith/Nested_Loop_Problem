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

For the time being, I am mainly interested in scenarios A and E and their associated probabilities, α and ε.

#### Approach  

I begin by assigning fixed values to α and ε: 

    alpha <-  0.70
    epsilon <- 0.05

I want to let the other probabilities -- β, γ, and δ -- loop through their various combinations.  In this way I actually get a distribution of expected values, and for the time being that is what I want.


#### Problem #1  


#### Problem #2  



#### Conclusion  
