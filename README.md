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

    1: alpha <-  0.50
    2: epsilon <- 0.05

Since α + β + γ + δ + ε = 1, it follows that γ + δ + ε = 1 - (α + β).

I want to let the other probabilities -- β, γ, and δ -- loop through their various combinations.  In this way I actually get a distribution of expected values, and for the time being that is what I want.

So I create a variable that will lay the groundwork for that:

    3: mid_percentages <- 1 - (alpha + epsilon)

With these particular initial values of alpha and epsilon, `mid_percentages` equals 0.45, which is what I expect.

Now I create a vector that will allow me to loop through the various possibilities:

    4: percentages <- seq(0, mid_percentages, .01)

That vector looks like this:

    5: [0.00, 0.01, 0.02, ..., 0.45]

Again, this is what I expect.

Now I'm ready to begin looping. (And in the spirit of Donald Knuth, I am not optimizing at this point. Later I'll look at the apply family, but not yet.)

Here is my nested loop:

    6: for(beta in percentages){
    7:   for(gamma in percentages){
    8:     for(delta in percentages){
    9:       if(beta + gamma + delta == mid_percentages){
    10:        do something
    11:       }
    12:     }
    13:   }
    14: }

And at this point, the `do something` in line 10 is:

    10:        print(paste0(beta, " ", gamma, " ", delta))

I am having two problems.

#### Problem #1  

The first problem is that when I run the print statement in line 10, I expect something like this: 

    0		0	0.45
    0		0.01	0.44
    0		0.02	0.43
    0		0.03	0.42

	and so on...
	
    0.45	0	0

And what I actually get is this:

    0 		0 	0.45
    0 		0.03 	0.42
    0 		0.09 	0.36
    0 		0.15 	0.3  
    
    	and so on...
	
    0.42	0 	0.03
    0.42 	0.03 	0
    0.45 	0 	0

A number of correct combinations of `beta`, `gamma`, and `delta` are being left out.

#### Problem #2  

The second problem -- which I discovered while trying to debug the first -- is that when I replace `mid_percentages` in line 9 with `0.45` I expect to get the exact same output, but instead I get this:

    0 		0.01 	0.44
    0 		0.02 	0.43
    0 		0.04 	0.41
    0 		0.05 	0.4
    0 		0.06 	0.39
    0 		0.07 	0.38  
    
    	and so on...
	
    0.43 	0 	0.02
    0.43 	0.01 	0.01
    0.43 	0.02 	0
    0.44 	0 	0.01
    0.44 	0.01 	0
    
Again, combinations are being left out, including the first and last that appeared when I used `mid_percentages`.
    
#### Conclusion  

Experience has shown me that this is probably some incredibly simple mistake, but that I've backed myself into a corner thinking about it and now can't see my way out.

The exact code I am running is [here](https://github.com/vmsmith/Nested_Loop_Problem/blob/master/code.R).
