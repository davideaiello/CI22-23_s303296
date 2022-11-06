# LAB 2

## Contributors
-  Davide Aiello (303296) 
-  Giuseppe Pellegrino (303999)


## Supporters

-  Leonardo Rolandi (301216)
-  Flavio Patti (301104)

## Project
The solution consists in a genetic algorithm, based on cross-over and mutation. As population we took just a sequence of zeroes with a random one. For each of index of list of lists given by the problem, at position i if you have one means that the algorithm take the element i of "problem".
The mutation consists simply in reverse the value of a random index in the genome (so if is 0 it'll change in 1).
The main part of this algorithm is the fitness function, the basic idea was to reward goal obviously and penalize genome length. after several attempts the solution that performs best in our case is this one: `(N - len(GOAL - set(list))) - numpy.sqrt(len(list))`, where the first member represent the number of distinct elements in the genome and the second is just the square root of the length of the genome. We tried also to penalize the number of repetition but it tourns out that the performs was worst than this.

## Parameters 

N stands for the number of problem generation.

GENETIC_OPERATOR_RANDOMNESS stands for mutation rate 

| Parameter                   | Value                                   |
| --------------------------- | --------------------------------------- |
| PROBLEM_SIZE                | Number of distinct elements of the list |
| POPULATION_SIZE             | N*2                                     |
| OFFSPRING_SIZE              | N*1.5                                   |
| NUM_GENERATION              | 1000                                    |
| TOURNAMENT_SIZE             | N/2                                     |
| GENETIC_OPERATOR_RANDOMNESS | 0.3                                     |



## Results

| N   | W    |
| --- | ---- |
| 5   | 5    |
| 10  | 13   |
| 20  | 36   |
| 50  | 89   |
| 100 | 196  |
| 500 | 1410 |

