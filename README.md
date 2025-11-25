# The 2025-2026 Computing Challenge: Percolation in Square Lattices



This year Computational Challenge revolves around writing a code to study the [**percolation problem**](https://en.wikipedia.org/wiki/Percolation_theory) on square lattices. Percolation theory is a fundamental concept in materials science, physics, and mathematics that describes the behavior of connected clusters in a random system. It has important applications in understanding phenomena such as **electrical conductivity in composite materials**, **fluid flow through porous media** and, **phase transitions**, and **network connectivity**. 

In particular, you will be asked to write a code to perform simulations to determine the **percolation threshold** - the critical probability at which a spanning cluster (a path connecting opposite edges of the lattice) first appears - for different connectivity rules on a square lattice.



## Problem description

You will study percolation on a **square lattice** of size $L \times L$, where $L$ is an integer (we recommend starting with $L=5$ for initial testing and visualisation). 

Each site (sometimes also called a node) in the lattice can be in one of two states: **active** or **inactive**. Each site $i$ is characterised by two indices $x_i$ and $y_i$ (think about this as their coordinates), where $x,y$ are integers in the interval $[0,L)$. 

### Connectivity Rules

You need to investigate 2 different connectivity scenarios between sites:

1. **First neighbors only**: Two active sites $i$ and $j$ are considered connected if they are nearest neighbours on the lattice. Mathematically, this means that the total difference between their indices $x$ and $y$ is 1: $\Delta_T = \Delta x + \Delta y = |x_i - x_j| + |y_i - y_j| = 1$. In a square lattice like the one you are studying, each site has 4 first neighbours (up, down, left, right directions).

2. **First and second neighbors**: Two active sites are connected if they are either first neighbours ( $\Delta_T = 1$ ) or second neighbours $\Delta_T = 2$. Each site has up to 8 neighbours total (4 first + 4 second neighbours).

In practice, if you visualise your lattice as a square grid, first neighbours share and edge, while second neighbours are along a diagonal. 

### Activation Mode

Each site on the lattice is independently activated with probability $p$, where $0 \leq p \leq 1$. Tip: `numpy.random` functions to randomly activate sites based on this probability.

### Percolation Detection

After you randomly assigned a state (active or inactive) to each site, you need to **write an algorithm that checks whether or not there is a continuous path connecting the top to the bottom edge of the lattice**. 

A system is said to **percolate** if there exists even a single one of such paths. For the purpose of this challenge, we will look at vertical percolation only (top to bottom).

Note that, mathematically, the top edge of the lattice is the set of sites $\{i\}$ for which $x_i = 0$ ($L$ for the bottom). Similarly, we can call the left or right side of the lattice the set of point for which $y_i=0$ (or $L$).

### Boundary conditions ###

For each system, you need to experiment with 2 different *boundary conditions*:

> 1. Fixed boundary conditions: sites at the leftmost and rightmost edges are only connected to internal nodes.
> 2. Periodic boundary conditions: there are no edges in this case, and sites on the leftmost edge are connected to those on the rightmost edge (at the same value of $y$), and vice versa. It is like if the lattice was drawn on a sheet, and the sheet was rolled up so that the two sides are connected to each other, forming a tube. Thus, any active site in the leftmost part of the lattice is considered connected to the right edge, and any active site in the rightmost column is considered connected to the left edge. 

### IMPORTANT ###

There is no single correct way to detect a percolation path. So please do take some time to think about how you can do it, and test if the algorithm you come up with works on simple cases. 

If you get stuck, feel free to Google for **percolation detection** algorithms. However, make sure that whatever you implement works for the specific instructions provided for this problem. 

As a suggestion: it might be easier to first identify all clusters of activated states in the system (a cluster being a group of sites that have at least one connection to each other), then check if any of the clusters vertically traverse the whole system.



## Visualing the result

 **Visualising what happens in the system can be of great help!** In your case, you can do that, for example, by adapting the following piece of code to print the position of the sites and their activation state. Here, red is active, black is inactive.



#Check what this piece of code does!
[Code Omitted]



## The Question to answer

**For each of the 4 different combinations of ( connectivity x boundary conditions ), what is the probability $p$ at which percolation occurs?**

### Important note ###

Each time you prepare a lattice (by randomly assigning activation states), even for the same probability of activation $p$, whether or not a percolation path will be observed is a random event. However, if we repeat the process many different times, the answer will actually converge to a well-defined value. In other words, a positive or negative answer to the question above is well-defined only in a statistical sense. 

Because of the above, you will have to write the code so that you can decide to prepare the system a user-defined number of times $N_{\mathrm rep}$ times, and experiment with different values for this quantity. 

We will say that the system percolates at a given $p$ value if the fraction $f$ of systems prepared with this $p$ value for which a percolating path is detected is at least $f\ge 0.5$, with an uncertainty of +/- 0.1. 

To estimate this fraction and its uncertainty, you need to:
1) "Prepare" the system $N_{\mathrm rep}$ times, each time randomly assigning activation state to all different sites with the same probability $p$. Measure the fraction of times for which a perculating path can be found.
2) Repeat step 1) $N_{\rm stat}$ times.
3) Your estimate of the fraction $f$ is the *average* calculated over the $N_{\rm stat}$ trials, and the variance of this quantity can be considered as a measure of your "uncertainty".



## Material to be submitted 

> 1) The code prepared to solve the challenge, either as a jupyter notebook or as a standard python file (if you know how to write one). 

> 2) A plot of the fraction of activated systems $f$ as a function of the single-site activation probability $p$, comparing in the same plot the 4 different combinations. To estimate this plot, use $L=50$.

> 3) 2 plots of the variance in the measured fraction $f$ as a function of lattice size (from L=10 to L=100) for $p = 0.25$ and $p=0.6$

> 4) A plot representing the state of the system for one example system (see the code provided above).



## Submission and marking 

**Only a single person per group will have to submit the code and the plots on behalf of the whole group**. 

However: 

**each single person should separately submit a peer-review** of the contribution of different team members (more below). 

The submission must be done via Blackboard.

The peer review evaluation, which can be done as a Word or text file, should be named "peer-review evaluation" and contain the names of your group components and, for each person, a mark of 0, 50 or 100 evaluating their contribution to the project (obviously, do not rate your own contribution...)

The final total mark you will receive will be 70% of the group mark for the exercise + 30% coming from the peer evaluation. **If a person has more than a single peer evaluation of 0%, this person will have their total mark set to 0**, unless specific mitigation circumstances can be provided.

### Marking criteria

> 1. Correct use of functions and their implementation, as well as correct use of the data types introduced in the lectures. **20 out of 100 Marks** 

> 2. Correct use of the control flow constructs introduced in the lectures. **20 out of 100 Marks** 

> 3. Appropriate structuring of the code into classes. **20 out of 100 Marks**

> 4. Use of the appropriate numpy functionalities. For example, you should avoid to re-code something that is already present in the library for you (at least if it is something we have seen in the course!). **20 out of 100 Marks** 

> 5. The code implements the various steps in a way that translates this problem into a correct algorithm to solve it **20 out of 100 Marks**



## Some remarks and How to go about solving this challenge:

- There is **not** a single solution in terms of how to structure the code. However, a well-structured code will probably be divided into classes, with specific attributes. 

- Try to structure the code using classes to build a hierarchical approach to the problem. For example, you might have a class "system" representing a single lattice in a specific state, and this class might have a method attribute "calculate_percolation" that takes the activation state of all lattice sites and determines if a percolating path is found. You might then have another "simulation" class that generates different objects of type "system", and uses a method "calculate_fraction()" to analyse these systems and return the fraction under percolation...and so on. 

- It is good practice to test each sub-part of the code independently to check that it works as an isolated unit before assembling them together. This will make sure that if there is a problem (because, for example, you obtain a nonsensical output), you know where it is, which makes it easier to correct it. 


- Although there is not a single recipe to write the code correctly and you will have to experiment a bit,  if you do not coordinate initially within the group, it will be much harder to combine all the various parts later. In particular, coordination is required because the input for one part of the code is the output for another, and they have to blend together efficiently.


### "Divide & Conquer" strategy to coding:

When you are about to solve a problem using a computational approach, there are a few steps typically involved. Some are related to how to face a complex problem in general, others to the fact that you should be doing that as a group and not alone.  
The general approach I would suggest you to use is the so-called "Divide and Conquer" approach, the (somewhat wrong) English translation of the ancient Romans motto [*Divide et Impera*](https://en.wikipedia.org/wiki/Divide_and_rule). In practice, the idea is to apply a centuries-old military strategy, whose philosophy can be simplified in this words: **When a problem seems to big to be tackled, first decompose it in smaller, simpler parts**. In this way, these smaller subparts can be more easily solved, one by one, and then re-assembled them together to find the solution of the initial problem. This is a general strategy that might be used in many situations and is **very common when dealing with complex scientific problems**.  

Let us translate this strategy into practical steps:

1. First, **read the whole text of the problem once all together**.
2. Read it a second time, to **identify the different subparts in which it can be split**. Ideally, you want each person in the group to code the solution for one of these blocks. 
3. Before each person starts to write code for their subproblem, it is important that you **coordinate together within the group and decide first which are the inputs and which are the outputs needed for each block, and their format**. This step is usually helped by starting to write the solution as pseudo-code, i.e., as a series of instructions, without worrying to use the correct synthax of the Python language (or for that matter any programming language you might wish to use). 

**Example of Pseudo-code** - for making a ["Tiramisu", a delicious Italian dessert](https://www.youtube.com/watch?v=87V4nizNJiE) 
1. Prepare the cream [INPUT: eggs whites, egg yolks, mascarpone, sugar; INSTRUMENT: mixer; OUTPUT: cream]
2. Prepare the Lady Fingers (a type of biscuits) [INPUT: biscuits, coffee, rum; INSTRUMENT: coffee machine; OUTPUT: basis for the tiramisu]
3. Assemble the cream and Lady Fingers together and top with cocoa [INPUT: Cream, Lady Fingers, Cocoa powder; INSTRUMENT: Hands OUTPUT: Tiramisu]
4. Enjoy & Eat!
