---
layout: post
title: "Discrete Optimization by The University of Melbourne"
categories: misc
author: "Ditikrushna Giri"
---

### Week 1 : 

**Practial Implementation Tip:**
 - **DFS Branch and Bound**
	- It pays off quite well to sort the inputs by either value, weight, or value/weight 
     - **Investigate:** The optimum stratergy should be to check the entropy of the field and choose the one with lowest 
  - **Dynamic Programming**
	  - It could be speeded up by using sparse tables to represent 	transition points
       - The pseudo-polynomial time concept can be understood by constructing a DP table for non-integral weight values ;)
- **Greedy Algorithms**
    - Pick one item at a time greedily with diff. heuristic.
    - Choose the smallest item first
	- Choose the most valuable item first
	- Better than the earlier methods? We can using the structure of problem
	- Value density, value per Kg ( Specific to Indiana Jones example )
	 - **Properties:**
		 - They give you a baseline
		 - No garuantee if we have an optimal situation (in general)
		 - The optimality of the solution depends upon the input
		 - In general, we can always try to solve a problem using greedy approach and then improve over it using other methods
