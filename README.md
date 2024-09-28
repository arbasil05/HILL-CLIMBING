# ExpNo 5 : Implement Simple Hill Climbing Algorithm
## Name: Abdur Rahman Basil A H
## Register Number: 212223040002

# Aim:
Implement Simple Hill Climbing Algorithm and Generate a String by Mutating a Single Character at each iteration

# Theory:
Hill climbing is a variant of Generate and test in which feedback from test procedure is used to help the generator
decide which direction to move in search space.
Feedback is provided in terms of heuristic function.

# Algorithm:
1. Evaluate the initial state. If it is a goal state, then return it and quit. Otherwise, continue with the initial state
as the current state.
2. Loop until a solution is found or there are no new operators left to be applied in the current state:
   a. Select an operator that has not yet been applied to the current state and apply it to produce a new state.
   b. Evaluate the new state:
      i. If it is a goal state, then return it and quit.
      ii. If it is not a goal state but better than the current state, then make the new state the current state.
      iii. If it is not better than the current state, then continue in the loop.

# Steps Applied:
### Step-1: Generate Random String of the length equal to the given String
### Step-2: Mutate the randomized string, each character at a time
### Step-3: Evaluate the fitness function or Heuristic Function
### Step-4: Loop Step-2 and Step-3 until we achieve the score to be Zero to reach Global Minima

# Program
```
import random
import string

def generate_random_solution(answer):
    # Find the length of 'answer' and store in 'l'
    l = len(answer)
    # Return a random list of characters of the same length as 'answer'
    return [random.choice(string.printable) for _ in range(l)]

def evaluate(solution, answer):
    print(solution)
    target = list(answer)
    diff = 0
    for i in range(len(target)):
        s = solution[i]
        t = target[i]
        # Calculate the "difference" between two strings, character by character.
        # ord(s) - ord(t) calculates the difference between ASCII values.
        # abs() ensures the difference is non-negative.
        diff += abs(ord(s) - ord(t))
    return diff

def mutate_solution(solution):
    # Select a random index in the solution to mutate
    ind = random.randint(0, len(solution) - 1)
    # Change the character at the selected index to a random printable character
    solution[ind] = random.choice(string.printable)
    return solution

def SimpleHillClimbing():
    answer = "Artificial Intelligence"
    # Generate a random initial solution
    best = generate_random_solution(answer)
    # Evaluate the score of the initial solution
    best_score = evaluate(best, answer)
    
    while True:
        print("Score:", best_score, " Solution:", "".join(best))
        # If the best score is 0, the goal state is reached
        if best_score == 0:
            break
        # Generate a new solution by mutating the current one
        new_solution = mutate_solution(list(best))
        # Evaluate the new solution
        score = evaluate(new_solution, answer)
        # If the new solution is better, update the best solution
        if score < best_score:
            best = new_solution
            best_score = score

# answer = "Artificial Intelligence"
# Uncomment the following lines for debugging or testing purposes
# print(generate_random_solution(answer))
# solution = generate_random_solution(answer)
# print(evaluate(solution, answer))
SimpleHillClimbing()
```
# Sample Input and Output
## Sample String: Artificial Intelligence
## Output:
Score: 643  Solution: 8RzF:oG ]%;CPORRMe!zGvk
Score: 609  Solution: 8RzF:oG ]%;CPqRRMe!zGvk
Score: 604  Solution: 8RzF:oG ]%;CPqRRMe!zGqk
Score: 594  Solution: 8RzF:oG ]%;CPqRRWe!zGqk
Score: 551  Solution: 8RzF:oGK]%;CPqRRWe!zGqk
 ...................................................
 ...................................................
 Score: 1   Solution: Artificial Intelligencf
 Score: 0   Solution: Artificial Intelligence
