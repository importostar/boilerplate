---
title: python_recursion_experiments
date: 2020-05-07
---
Example Python program python_recursion_experiments.py


## Methods

* def should_successfully_count_fewest_jumps_to_goal(fn, tests=[(9,2),(13,2),(19,4)],longer_tests=[(34,3),(43,5)]):
* def recursion_bottomup_goaltestpre(goal_distance=20, start_distance = 1, jump_lengths = [1,4,5,11]):
* def recurse(distance=start_distance, count=0):
* def recursion_bottomup_goaltestin(goal_distance=20, start_distance = 1, jump_lengths = [1,4,5,11]):
* def recurse(distance=start_distance, count=0):
* def recursion_cached_bottomup_goaltestin(goal_distance=20, start_distance=1, jump_lengths=[1,4,5,11], fewest_jumps={}):
* def recurse (distance=start_distance, count=0):
* def looping_cached_bottomup_goaltestin(goal_distance=20, start_distance=1, jump_lengths=[1,4,5,11], fewest_jumps={}):
* # def ensureValidStart(goal_distance,start_distance=1,jump_lengths=[1,4,5,11]):

## Code

Python example

    # Deep Dive into recursion and looping solutions for optimization problems
    # Written to help me describe optimization functions' parts, and those parts' permutations,
    # to facilitate both making choices between them and effectively articulating those choices
    
    ##
    # Code Design
    ##
    # - function parts broken down completely
    # - only one thing can change per example. Even identical variable names describe identical things in all examples
    # - full word variables to save limited working memory for learning (vs storing variable semantics)
    #     (1. all functions "jump" from "start_distance" to "goal_distance" in the "fewest_jumps" possible)
    #     (2. all functions "i" from "a" to "n" in the "x" possible)
    # - only the minimum variables necessary for the permutation to run
    # - all the code runs (tested with asserts in the file)
    
    
    
    
    ##
    # Permutation Definitions
    # NOTE: Each function has one permutation of all of these
    #       If you write a function I haven't added and/or think of a missing permutation, please add them to the comments.
    ##
    
    # - PROGRESSION STRATEGY (Recursion|Looping)
    # - CACHED (cached) - intermittent results are cached/memoized, or not
    # - DIRECTION (bottom-up|top-down)
    # - GOAL TEST LOCATION pre|in|post "loop"
    #     note that "loop" is used twice, once for the test location, and once for the "looping" strategy
    #     Please comment if you know better language that differentiates the two
    # ... Permutations with names and concepts I'm still disentangling
    # - ______ ? VARIABLE TYPES I don't know if there are standard names for different types of variables.
    #             e.g, distance is ____? count is ___? jump_lengths is ___? Maybe Independent vs dependent variables?
    # - ______ ? VARIABLE PLACEMENT like dependent in an inner loop and independent in outer (if it matters)
    # - _______? ROOT (one|multi) (from a graph standpoint, one or multiple nodes can be a start)
    # - _______? TEST STRATEGY___? look behind vs look ahead when testing for the goal... or in recursion, when "wasted" function calls happen
    # - _______? ENTRY CONDITIONS (still hashing out what I even mean by this)
    # - ____anything-else____?
    
    
    
    ##
    # Test (Just one, since all examples thus far do the same thing in different ways)
    ##
    def should_successfully_count_fewest_jumps_to_goal(fn, tests=[(9,2),(13,2),(19,4)],longer_tests=[(34,3),(43,5)]):
        for pair in tests:assert(fn(pair[0])==pair[1]);
        for pair in longer_tests:assert(fn(pair[0])==pair[1]);
    
    
    
    
    
    ##
    # Constants
    ##
    
    BABY_JUMPS = 10000 # the number of jumps a baby took to go some distance.  Used for defaults and worst case comparisons.
    # ^^ Please ignore ethics and practicality of getting a baby to jump. That many times.
    
    
    
    
    
    
    ##
    # Functions
    ##
    
    
    ## Permutation: recursion|bottom-up|goal-test-pre
    def recursion_bottomup_goaltestpre(goal_distance=20, start_distance = 1, jump_lengths = [1,4,5,11]):
        
        def recurse(distance=start_distance, count=0):
            if(distance == goal_distance): return count
            if(distance >  goal_distance): return BABY_JUMPS
            return min(recurse(distance + jump, count + 1) for jump in jump_lengths)
        
        jumps_to_goal = recurse()
        return jumps_to_goal
    
    should_successfully_count_fewest_jumps_to_goal(recurseBottomUpGoalTestPreLoop,longer_tests=[])
    ## Permutation: recursion|bottom-up|goal-test-in
    def recursion_bottomup_goaltestin(goal_distance=20, start_distance = 1, jump_lengths = [1,4,5,11]):
        
        def recurse(distance=start_distance, count=0):
            if(distance == goal_distance): return count
            return min(recurse((distance+jump,count+1) for jump in jump_lengths if distance+jump <= goal_distance),default=BABY_JUMPS)
        
        jumps_to_goal = recurse()
        return jumps_to_goal
    
    should_successfully_count_fewest_jumps_to_goal(recursion_bottomup_goaltestin,longer_tests=[])
    ## Permutation: recursion|bottom-up|goal-test-post
    ## Permutation: recursion|top-down|goal-test-pre
    ## Permutation: recursion|top-down|goal-test-in
    ## Permutation: recursion|top-down|goal-test-post
    ## Permutation: (impossible) looping|bottom-up|goal-test-pre
    ## Permutation: (impossible) looping|bottom-up|goal-test-in
    ## Permutation: (impossible) looping|bottom-up|goal-test-post
    ## Permutation: (impossible) looping|top-down|goal-test-pre 
    ## Permutation: (impossible) looping|top-down|goal-test-in
    ## Permutation: (impossible) looping|top-down|goal-test-post
    # These ^^ looping permutations are impossible to get consistent optimal results from.
    # Without a cache, they form greedy functions.  Why do the recursive ones yield optimal results?
    # Recursively nested function scopes implicitly cache all results along their recursion path.
    # Each min() call compares the results at each cache distance. (like the combine phase of merge sort)
    
    ## Permutation: cached|recursion|bottom-up|goal-test-pre
    ## Permutation: cached|recursion|bottom-up|goal-test-in
    def recursion_cached_bottomup_goaltestin(goal_distance=20, start_distance=1, jump_lengths=[1,4,5,11], fewest_jumps={}):
        should_cache = lambda distance,count: distance not in fewest_jumps or count<fewest_jumps[distance]
        
        def recurse (distance=start_distance, count=0):
            fewest_jumps[distance] = count
            if(distance==goal):return count
            return min((recurse(distance+jump, count+1) for jump in jump_lengths if distance<=goal and should_cache(distance+jump,count+1)),default=BABY_JUMPS)
        
        jumps_to_goal = recurse()
        return jumps_to_goal
    
    should_successfully_count_fewest_jumps_to_goal(recursion_cached_bottomup_goaltestin)
    ## Permutation: cached|recursion|bottom-up|goal-test-post
    ## Permutation: cached|recursion|top-down|goal-test-pre
    ## Permutation: cached|recursion|top-down|goal-test-in
    ## Permutation: cached|recursion|top-down|goal-test-post
    ## Permutation: cached|looping|bottom-up|goal-test-pre
    ## Permutation: cached|looping|bottom-up|goal-test-in
    def looping_cached_bottomup_goaltestin(goal_distance=20, start_distance=1, jump_lengths=[1,4,5,11], fewest_jumps={}):
        should_cache = lambda distance,count: distance not in fewest_jumps or count<fewest_jumps[distance]
        
        fewest_jumps[start_distance]=0
        for distance in range(start_distance,goal_distance+1):
            count=fewest_jumps[distance]
            for jump in jump_lengths:
                if should_cache(distance+jump, count+1): fewest_jumps[distance+jump]=count+1
        
        jumps_to_goal = fewest_jumps[goal_distance]
        return jumps_to_goal
    
    should_successfully_count_fewest_jumps_to_goal(looping_cached_bottomup_goaltestin)
    ## Permutation: cached|looping|bottom-up|goal-test-post
    ## Permutation: cached|looping|top-down|goal-test-pre
    ## Permutation: cached|looping|top-down|goal-test-in
    ## Permutation: cached|looping|top-down|goal-test-post
    
    
    
    
    # 
    # def ensureValidStart(goal_distance,start_distance=1,jump_lengths=[1,4,5,11]):
    #     if(start_distance < 0 or start_distance > goal_distance): raise ValueError("start must be in interval [0,n]")
    #     if(len(jump_lengths)==0): raise ValueError("jump_lengths cannot be empty")
    #     if not min(goal_distance % jump for jump in jump_lengths) == 0:
    #          raise ValueError("goal_distance not reachable from given jump_lengths")
    #     jump_lengths = sorted(jump_lengths)
    #     if(goal_distance<jump_lengths[0]): raise ValueError("goal_distance must be >= the smallest jump_length")
    # 
    #     BABY_JUMPS = 10000 # the number of jumps a baby took to get to ___ (used for defaults and worst cases)
    #     cache = {}
    #     return goal_distance,start_distance,jump_lengths,BABY_JUMPS,cache

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
