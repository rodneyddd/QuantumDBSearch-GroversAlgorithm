# QuantumDBSearch-GroversAlgorithm
A quantum algorithm used to accelerate database searches.

# WHY:

So, in middle school I actually wanted to become a quantum physicist. Around that time my love for computer science also bloomed. So naturally, quantum computing became a field for me to look into. I've been interested in quantum computing for a while, and I've actually been taking Brilliant Courses for Quantum Computing to prepare myself for this project.


# WHAT:

## What is Quantum Computing: 

Quantum Computing is a form of computing designed to tackle problems that are similar to quantum mechanics solutions. Some problems are easier to map onto quantum mechanics like quantum simulations, others are harder to map onto quantum mechanics like convential data sorting & searching algorithms. These are places where the problem doesn't naturally align with quantum principles. And therefore isn't ideal to map to quantum mechanics. But I'm going to attempt it using an algorithm designed by Lov Kumar Grover called Grover's algorithm. He was born in 1961 and designed the algorithm in 1996.

## Grover's Algorithm

Grover's algorithm is a quantum algorithm that can search for an item within a group of elements in O(√ N) time. For reference, classical computers ususally take O(N) time, as they need to search the entire group to see the whole thing.

## What I'm trying to do:
So the goal is to try and implement this algorithm to try and optimize database query searches.


# HOW:

The first step is create a quantum oracle. 
> First off doesn't that sound ridiculously cool?!!

A Quantum Oracle is an operation that marks or highlights the qubits representing the target item, making them distinguishable from the rest of the states.
The thing about quantum computing is that this form of computing is based off of probabilistic states, and therefore we're dealing with a bunch of states that have a probability of being active at the same time (superposition). But are specifically looking at which one has the highest probability of being active at any given time. 

Within the oracle the input state corresponds to the target item, as in when the program recognizes the target item, the oracle applies a phase shift of -1. This flips the signs of the amplitude by -1. All other amplitudes are left unaffected.

(This is what the X Gate is responsible for).


Then comes something called the Diffusion Operator, which makes it easier to pinpoint the specific target item. Throughout the array of qubits we apply the Z gate. The Z gate sets up the quantum state by creating a state where marked items have a phase difference from unmarked items, facilitating the interference and amplification of the marked items during the algorithm's execution.

Then we apply the H gate. The H gate puts the qubits into a superposition state.

Superposition enables interference effects between different paths in the quantum state. 
Something called a constructive interference occurs when this transformation hits the marked items. It ends up increasing the probability of measuring those states. The amplitudes add up, leading to a higher probability for specific outcomes. All the other unmarked items have a destructive interference where if they aren’t flagged or marked their amplitudes cancel each other out, resulting in a lower probability for the inputs that don't match the target item. 

In the Grover’s Search operation, we go through an array of qubits, we apply a H gate to them, which puts them in a state of superposition, and we iterate through them and apply the previous functions multiple times until we’re done iterating. Then we save the results of the array and return it. It’s in the testing file, that we use the resulting array to find the marked item.

