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

### Alternative
I also wrote an alternative with respect to the previous part in which a genome is made off two parameters, alpha and beta. This two parameter determine the strategy which will be played based on the range in which they fall(see the function ``build_strategy``). The idea in this case is not starting from already hard coded rules but exploit very simple choices in order to find a sort of their combination which can provide a good result.
In this case I didn't take into account the bound k.

For example, againts `pure_random`, we obtain this result:

- the best winrate is 68.0 with paramter: alpha 0.3 - beta 0.72


## 3) MinMax
In order to write the minmax strategy I started from this code found online:

```
def minimax(state, max_turn):
    if state == 0:
        return 1 if max_turn else -1
    possible_new_states = [
        state - take for take in (1, 2, 3) if take <= state
    ]
    if max_turn:
        scores = [
            minimax(new_state, max_turn=False)
            for new_state in possible_new_states
        ]
        return max(scores)
    else:
        scores = [
            minimax(new_state, max_turn=True)
            for new_state in possible_new_states
        ]
        return min(scores)
```

It takes into account one row with at most 3 possible moves starting from the actual one and considering as a winner whom leaves the last object.
Then I extended it taking into account all the possible moves on the board and a value of depht in order to reduce the computational cost.
I also adding a small change on the strategy: if the minmax function is not able to find any value of 1 (which means a good move on the road to win), it picks a random move.

Here we are different result with `MIN_SIZE` = 4 and `depth` = 3. k was putted to a value eual to 100 in order to not be taked into account.

##### Results vs pure random
- INFO:root:NUM_MATCHES : 10 - ratio as player1: 80.0, ratio as player2: 80.0
- INFO:root:NUM_MATCHES : 50 - ratio as player1: 94.0, ratio as player2: 92.0
- INFO:root:NUM_MATCHES : 100 - ratio as player1: 93.0, ratio as player2: 93.0

##### Results vs shortest row
- INFO:root:NUM_MATCHES : 10 - ratio as player1: 70.0, ratio as player2: 90.0
- INFO:root:NUM_MATCHES : 50 - ratio as player1: 88.0, ratio as player2: 86.0
- INFO:root:NUM_MATCHES : 100 - ratio as player1: 89.0, ratio as player2: 89.0

##### Results vs optimal strategy
- INFO:root:NUM_MATCHES : 10 - ratio as player1: 0.0, ratio as player2: 0.0
- INFO:root:NUM_MATCHES : 50 - ratio as player1: 0.0, ratio as player2: 4.0
- INFO:root:NUM_MATCHES : 100 - ratio as player1: 0.0, ratio as player2: 3.0

If we try without the `depth` and with `MIN_SIZE`= 3, we obtain those results against the optimal strategy:
- INFO:root:NUM_MATCHES : 10 - ratio as player1: 100.0, ratio as player2: 0.0
- INFO:root:NUM_MATCHES : 50 - ratio as player1: 100.0, ratio as player2: 0.0
- INFO:root:NUM_MATCHES : 100 - ratio as player1: 100.0, ratio as player2: 0.0


## 4) Reinforcement learning
In order to accomplish this task, I took into account the code related to the Maze, given by the professor, and then I adapted it to the Nim game. I used the Agent class and I slighted modified the Nim class. I choose to implement the code by exploiting three different rewards:
- -1 if the move leads me to a defeat
- 0 if the move doesn't terminate the game
- 1 if the move leads me to a victory

Then I evaluated the number of set of matches needed to reach a convergence value for the win rate. Each set consists in 100 games. 
The agent starts as second player and I didn't take into account k.
`NIM_SIZE` = 7

##### Results vs dummy strategy
- INFO:root: 0: 52.0
- INFO:root: 20: 56.99999999999999
- INFO:root: 40: 99.0
- INFO:root: 60: 97.0
- INFO:root: 80: 100.0
- INFO:root: 100: 100.0
- INFO:root: 120: 100.0

##### Results vs shortest row
- INFO:root: 0: 17.0
- INFO:root: 20: 42.0
- INFO:root: 40: 100.0
- INFO:root: 60: 100.0
- INFO:root: 80: 100.0

##### Results vs my strategy
- INFO:root: 0: 42.0
- INFO:root: 20: 38.0
- INFO:root: 40: 89.0
- INFO:root: 60: 84.0
- INFO:root: 80: 95.0
- INFO:root: 100: 89.0
- INFO:root: 120: 85.0
- INFO:root: 140: 86.0
- INFO:root: 160: 81.0
- INFO:root: 180: 90.0
- INFO:root: 200: 85.0
- INFO:root: 220: 81.0
- INFO:root: 240: 82.0
- INFO:root: 260: 86.0
- INFO:root: 280: 88.0

##### Results vs pure random
- INFO:root: 0: 49.0
- INFO:root: 20: 43.0
- INFO:root: 40: 56.0
- INFO:root: 60: 41.0
- INFO:root: 80: 49.0
- INFO:root: 100: 48.0
- INFO:root: 120: 47.0
- INFO:root: 140: 46.0
- INFO:root: 160: 46.0
- INFO:root: 180: 53.0
- INFO:root: 200: 43.0
- INFO:root: 220: 47.0
- INFO:root: 240: 48.0
- INFO:root: 260: 45.0
- INFO:root: 280: 53.0

`NIM_SIZE` = 4
##### Results vs optimal strategy
- INFO:root: 0: 3.0
- INFO:root: 20: 0.0
- INFO:root: 40: 1.0
- INFO:root: 60: 0.0
- INFO:root: 80: 0.0
- INFO:root: 100: 0.0
- INFO:root: 120: 0.0
- INFO:root: 140: 0.0
- INFO:root: 160: 0.0
- INFO:root: 180: 0.0
- INFO:root: 200: 0.0
- INFO:root: 220: 0.0
- INFO:root: 240: 0.0
- INFO:root: 260: 0.0
- INFO:root: 280: 0.0