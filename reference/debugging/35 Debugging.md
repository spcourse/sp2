# Monitoring and debugging

A simulation is used to gain a picture of real scenarios, so the outcomes can be used in the 'real world'. It's effectively a *model*. 

It is often hard to know a simulation performed correctly simply by looking at the outcome. In the case of the apple before, you can analytically calculate the outcome. But it quickly becomes cumbersome.

That's why it is so important to systematically check a simulation. Here are a few pointers that should aid in doing so:

1. Check using pen and paper whether the core of your calculation is correct: are you working towards the right direction? If it becomes too complicated it's sometimes better to make a rough estimation and compare that to your simulation.

2. Have you looked up the correct constants and formulas? Verify them another time. Are the constants precise enough? A rounding error can compound incredibly quick!

3. Are your time steps sufficiently small?

4. Are the components of the simulation in the correct order? Make sure each step correctly calculates all values anew. Only when that is done check the values for any interesting milestone.

Finally a tip for debugging a simulation. You can print all values at each time step. Then you can precisely inspect them and see if an error occurred at some point. Or maybe the starting values were already incorrect!
