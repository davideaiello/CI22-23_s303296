# Description of the Game (Wikipedia)
Nim is a mathematical game of strategy in which two players take turns removing objects from a distinct heap or piles. On each turn, a player must remove at least one object, and may remove any number of objects provided they all come from the same heap or pile.
- `Goal: in order to win we need to take the last object`

# Solutions & Results
## 1) My Solution

- Game played: we play `10`, `100`, `1000` games vs differents opponents
- `NIM_SIZE` number: a random value from `5 to 13`
- Upperbound `k` of objects taken at each round: a random value from `2 to (NIM_SIZE - 1) * 2 +1` (there is no bound)
- The file of task 1 is `1_my_solution.ipynb`
- The games have been player starting as `first player` (starts with first move) or `second player` (starts with second move)
- I Nim Class is the one used in by professor

Description

- `my_strategy`: really simple strategy that find all the possibles moves then selects a random row and takes always
at least k objects. If there is no upperbound for that row, it takes all of the objects.
If there are no rows with more then one object, it starts to take one object random from the remained rows. 

##### I played against different strategies
- `pure_random`: pick a random row and select random objects (objects < k)
- `shortest_row`: take the shortest row and select random objects if row elements > k otherwise close the row selecting all objects
- `optimal_solution`: nim-sum solution used by professor in class that use brute force

##### Results vs shortest row
- INFO:root:NUM_MATCHES : 10 - ratio as player1: 0.0, ratio as player2: 100.0 with k : 12 (NIM_SIZE = 7)
- INFO:root:NUM_MATCHES : 100 - ratio as player1: 83.0, ratio as player2: 9.0 with k : 11 (NIM_SIZE = 12)
- INFO:root:NUM_MATCHES : 1000 - ratio as player1: 93.6, ratio as player2: 0.0 with k : 13 (NIM_SIZE = 9)

##### Results vs pure random
- INFO:root:NUM_MATCHES : 10 - ratio as player1: 40.0, ratio as player2: 70.0 with k : 7 (NIM_SIZE = 5)
- INFO:root:NUM_MATCHES : 100 - ratio as player1: 62.0, ratio as player2: 62.0 with k : 6 (NIM_SIZE = 5)
- INFO:root:NUM_MATCHES : 1000 - ratio as player1: 64.2, ratio as player2: 61.3 with k : 3 (NIM_SIZE = 13)

##### Results vs optimal strategy
- INFO:root:NUM_MATCHES : 10 - ratio as player1: 10.0, ratio as player2: 10.0 with k : 3 (NIM_SIZE = 5)
- INFO:root:NUM_MATCHES : 100 - ratio as player1: 0.0, ratio as player2: 1.0 with k : 8 (NIM_SIZE = 8)
- INFO:root:NUM_MATCHES : 1000 - ratio as player1: 5.9, ratio as player2: 6.8 with k : 5 (NIM_SIZE = 13)

## 2) Evolution Algorithm
- The file of task 2 is `2_GA.ipynb` 
- For this task I've been working with: [Gabriele Greco - Github](https://github.com/GabriG23/computational-intelligence-2022-2023-s303435). I had the idea of using evolutionary algorithm in order to find the best strategy to play the game, and then we coded together the solution
- I Nim Class is the one used in by professor
- population_size = `20`, offspring_size = `10`, num_generations = `100`, tournament_size = `2`, genetic_operator_randomness for mutation = `0.7`
- `Number of games` played: `100`
- `Rows` number: `11`
- Upperbound `k` of objects taken each round: `6`

Description
- For our solution we used a genetic algorithm. The population individuals are compose by the fitness value and 5 genome values from 0 to 1, one for each strategy, the bigger the value is the more the system will converge to that strategy. The mutation selected randomically which strategy to mutate recalculating the genome weight (we used a weighted average). One of the important function of our program is `compute_fitness` that compute the fitness which is the number of games won vs our opponent. In the end we combine the genetic information we use `uniform_cross_over` that based of the value of i put information of parent1 or parent2.

##### Differents strategy used
1. `shortest_row`: take the shortest row and select random objects if row elements > k otherwise close the row selecting all objects
2. `Davide_strategy`: is the my_strategy use in task 1 (see above the description)
3. `GabriG_strategy`: is really simple strategy that select the shortest row and it does 3 different operations 
    depending on the value of objects:
    1. if objects <= k: close the row selecting all the objects
    2. if objects > k*2: select k objects
    3. if objects between (k) and (k*2) it (select row elements - k) objects
4. `longest_row`: take the longest row and select random objects if row elements > k otherwise close the row selecting all objects
5. `pure_random`: pick a random row and select random objects (objects < k)

##### We played against
- `pure_random`: pick a random row and select random objects (objects < k)
- `optimal_solution`: nim-sum solution used by professor in class that use brute force

##### Results for pure random
- INFO:root:The best strategy is<function GabriG_strategy> with 100.0% winrate (fitness)
##### Results optimal strategy
- INFO:root:The best strategy is<function GabriG_strategy> with 100.0% winrate (fitness)

## 3) MinMax
- Working in progress

## 4) Reinforcement learning
- Working in progress