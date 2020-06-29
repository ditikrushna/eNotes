---
layout: post
title: "Mathmatical Optimization"
categories: misc
author: "Ditikrushna Giri"
---



### Overview of Optimization 

Mathmematical programming : 
- MP Techniques : Linear programming , Integer programming, mixed-integer programming,etc.  
- The different techniques address different types of problem. 

Constraint programming : 
- CP is especially appropriate for detailed scheduling problems and certain conbinatorial optimization problems . 


Typical optimization model development cycle : 

Define the scope **->** Identify objectives , variables and constraints **->** Gather data and create and test a prototype **->** Edit the model based on test results **->** Create and test a complete instance of the model **->** Adjust the model . 

Objective Function : 
- The objective function is a mathmatical representaion of the business objectives or goals to be achieved . 
- Objective functions alwayes start with the words "maximize" or "minimize" .
- Objective functions can be simple expression involving a singel objective or a more complex expression combining several objectives . 

Decison Variables : 
- Decison variables represent values or decisons that can be changed to arrive at the best solution possible value of the objective functions . 
- The value of decision variables are determined during the solution process . 
- Decison variebales have a **domain , bounds** and a **type** . 
- It is important to choose the decison variables well: they impact the formulation of the constraints . 

Constraints : 
- Constraints define the relationship between different decison variables.
- They represent the limits within which the solution should exit. 
- Constraints are either hard or soft : 
		- **Hard constraints** should not be violated under any circumstances.
		-  **Soft constraints** can be violated under certain circumstainces .

Feasibility vs Optimality : 
- A **feasible** solution is a solution that satisfies all the constraints . 
- An **optimal** solution is a feasible solution with the best possible value of the objective function .
- An **infeasible** solution is a solution where one or more constraints are violated .
- An **unbounded** solution is a solution to a problem where the constraints are not completely descibed , resulting in an objective that goes to plus or minus infinity . 


### (Linear Programming )Chapter 2 :
 Learning Objectives : 
 - The basic characteristics of a linear program.
 - How to analyze a simple production problem in terms of deceison variables , an objective function , and constraints .
 - Some algorithms used for optimization problems . 
 


