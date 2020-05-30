---
layout: post
title: "CPC Test NITT (Temp. Post)"
categories: misc
author: "Ditikrushna Giri"
---


## LEU - KGX 1
This problem was inspired by the Code Con Challenger Series question "Travel to the West" https://codecon.bloomberg.com/challenger-series/3902.

Leetcode 797 - https://leetcode.com/problems/all-paths-from-source-to-target/ was also useful in order to generate all possible paths.

It is useful to use some form of graph representation like an adjacency list in order to solve this problem.



    import math
    import os
    import random
    import re
    import sys
    import collections 
    
 
    
    def calculate_ways(routes):
    
        graph = generate_graph(routes)
        ways_to_london = calculate_unique_paths(graph, "LEU", "KGX")
        
        if (len(ways_to_london) == 0):
            print("NO ROUTES BETWEEN LEUCHARS AND LONDON KINGS CROSS")
            sys.exit()
            
        for possible_way in ways_to_london:
            print(possible_way)
        
    # This function will return a graph which converts the routes array that has been passed into an
    # adjacency list 
    def generate_graph(routes):
        
        graph = collections.defaultdict(list)
        
        for route in routes:
            source, destination = route.split()
            graph[source].append(destination)
    
        return graph
    
    
    # dfs traversal solution, function will be called repeatedly until destination is discovered and then backtrack
    # algorithm derived from https://leetcode.com/problems/all-paths-from-source-to-target/solution/
    def calculate_unique_paths(graph, source, destination):
        def solve(node):
            # if condition is met algorithm will backtrack
            if node == destination: return [destination]
            
            ans = []
            
            for nei in graph[node]:
                
                #  now exploring neighbours of node the path has been called at
                #  the answer is {node} + {path from nei to destination}
                
                for path in solve(nei):
                    ans.append(str(node) + "->" + str(path))
                    
            return ans
    
        # returning a sorted list of paths, that are not repeated
        return sorted(list(set(solve(source))))
    
    if __name__ == '__main__':
        routes_count = int(input().strip())
    
        routes = []
    
        for _ in range(routes_count):
            routes_item = input()
            routes.append(routes_item)
    
        calculate_ways(routes)
     





## LEU - KGX 2

This problem can be solved using a graph. It is also important to notice that the number of stations is small so the number of start and end combinations will be small compared to the maximum possible number of routes. This will indicate that some trains between a particular source to destination could be faster while others will be slower. The fastest route between two nodes will always be preferred and hence only this needs to be stored.

Once an appropriate graph has been created, the shortest path can be calculated using several shortest path finding algorithms.
    #!/bin/python3
    
    import math
    import os
    import random
    import re
    import sys
    import collections 
    
    
    all_nodes = set()
    
    def generate_graph(routes):
        graph1 = collections.defaultdict(dict)
    
        # Due to the number of source destination pairs being considerably less
        # than the number of routes we will get repeats in a traditional adjacency list representation
        source_destination_pairs = set()
    
        for route in routes:
            source, destination, distance = route.split()
            if (source, destination) in source_destination_pairs:
                curr_fastest_train_time = graph1[source][destination]
                # storing only fastest train time
                graph1[source][destination] = min(int(distance), curr_fastest_train_time)
            else:
                graph1[source][destination] = int(distance)
            all_nodes.add(source)
            all_nodes.add(destination)
            source_destination_pairs.add((source, destination))
    
        # simplifying representation of graph 1 to a more traditional adjacency list
        # but with a list of tuples, where each tuple stores the destination and the
        # fastest train time to that destination
        graph2 = collections.defaultdict(list)
        for source in graph1:
            for destination in graph1[source]:
                fastest_train_time = graph1[source][destination]
                graph2[source].append((destination, fastest_train_time))
    
        return graph2
    
    # calculating the shortest path from origin to destination
    def shortest_path(graph, origin, destination):
        distances = {node: float('inf') for node in all_nodes}
    
        # starting at origin node and hence distance to origin is set as 0
        distances[origin] = 0
    
        # keeping track of discovered and undiscovered nodes
        unseen, visited = all_nodes, set()
    
        # finding shortest path using dijkstra
        while unseen:
    
            # finding the node which is at the closest distance that hasn't been explored
            u = None
            for node in unseen:
                if u is None or distances[node] < distances[u]:
                    u = node
    
            # updating unseen and visited as u is now being explored
            unseen.remove(u)
            visited.add(u)
    
            for node, dist in graph[u]:
                if node in unseen:
                    # finding minimum distance to the node
                    distances[node] = min(distances[node], distances[u] + dist)
    
        return distances[destination]
    
    def fastest_route(routes):
        graph = generate_graph(routes)
        return shortest_path(graph, "LEU", "KGX")
    
    if __name__ == '__main__':
        fptr = open(os.environ['OUTPUT_PATH'], 'w')
    
        routes_count = int(input().strip())
    
        routes = []
    
        for _ in range(routes_count):
            routes_item = input()
            routes.append(routes_item)
    
        result = fastest_route(routes)
    
        fptr.write(str(result) + '\n')
    
        fptr.close()




## LEU - KGX 3 1 

One possible approach to solve this problem is using Dynamic Programming.

The student has a few choices each day he/she is travelling. At a particular day a student can hold a single ticket, weekly, monthly or annual season ticket.

Minimising cost at each day travelled after sorting the array passed into the function will result in the correct answer at the last day the student chooses to travel. The dp array will be storing the minimum cost of travel up until each day the student wanted to travel.


    #!/bin/python3
    
    import math
    import os
    import random
    import re
    import sys
    import bisect
    def solve(days_travelling):
        costs = [100, 399, 999, 4999]
        days_travelling.sort()
        n = len(days_travelling)
        dp = [0] + [float('inf')] * n
        for i in range(n):
            # finding out index from for a potential weekly pass and month pass will start ending at and including days_travelling[i]
            week_pass_start_index = bisect.bisect_right(days_travelling, days_travelling[i] - 7)
            month_pass_start_index = bisect.bisect_right(days_travelling, days_travelling[i] - 30)
    
            dp[i + 1] = min(dp[i] + costs[0],
                            dp[week_pass_start_index] + costs[1],
                            dp[month_pass_start_index] + costs[2])
    
        # annual pass option can only be selected once and will cover all days
        return min(dp[-1], costs[-1])  


