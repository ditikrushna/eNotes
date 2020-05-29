---
layout: post
title: "CPC Test NITT (Temp. Post)"
categories: misc
author: "Ditikrushna Giri"
---


## LEU - KGX 1



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
     





## Heads and Tails 
    #include <cmath>
    #include <cstdio>
    #include <vector>
    #include <iostream>
    #include <algorithm>
    using namespace std;
    
    
    int main() {
      
        int n;
        cin >> n ;
        
        vector<string> a(n);
        vector<int> dp(n);
        
        int heads = 0;
        
        for(int i = 0; i < n; ++i) {
            cin >> a[i];
            
            if(a[i] == "H") heads++;
        }
        
        if(a[0] == "H") {
            dp[0] = -1;
        } else {
            dp[0] = 1;
        }
        
        for(int i = 1; i < n; ++i) {
            if(a[i] == "H") {
                dp[i] = max(dp[i-1] - 1, -1);
            } else {
                dp[i] = max(dp[i-1] + 1, 1);
            }
        }
        
        cout << *max_element(dp.begin(), dp.end()) + heads << endl;
        
        return 0;
    }

## Shortest Path in Maze
    #include <cmath>
    #include <cstdio>
    #include <vector>
    #include <iostream>
    #include <algorithm>
    #include <queue>
    using namespace std;
    
    struct path {
        int row;
        int col;
        int dist;
    };
    
    int main() {
        int m,n;
        cin >> m >> n;
        int startr,startc,endr,endc;
        cin >> startr >> startc >> endr >> endc;
        vector<string> grid;
        for(int i = 0; i < m; i++) {
            string row;
            cin >> row;
            grid.push_back(row);
        }
        queue<path> bfs;
        path sp;
        sp.row = startr;
        sp.col = startc;
        sp.dist = 0;
        bfs.push(sp);
        vector< vector<bool> > visited;
        for (int i = 0; i < m; i++) {
            vector<bool> vr;
            for (int j = 0; j < n; j++) {
                vr.push_back(false);
            }
            visited.push_back(vr);
        }
        int md = -1;
        while (!bfs.empty()) {
            path curPath = bfs.front();
            bfs.pop();
          //  cout << "bfs at " << curPath.row << " " << curPath.col << "\n";
            visited[curPath.row][curPath.col] = true;
            if (curPath.row == endr && curPath.col == endc && (md == -1 || curPath.dist < md)) {
                md = curPath.dist;
            }
            if (curPath.row > 0 && grid[curPath.row-1][curPath.col] != '1' && !visited[curPath.row-1][curPath.col]) {
                path np;
                np.row = curPath.row-1;
                np.col = curPath.col;
                np.dist = curPath.dist+1;
                visited[curPath.row-1][curPath.col] = true;
                bfs.push(np);
            }
            if (curPath.col < n-1 && grid[curPath.row][curPath.col+1] != '1' && !visited[curPath.row][curPath.col+1]) {
                path np;
                np.row = curPath.row;
                np.col = curPath.col+1;
                np.dist = curPath.dist+1;
                visited[curPath.row][curPath.col+1] = true;
                bfs.push(np);
            }
            if (curPath.row < m-1 && grid[curPath.row+1][curPath.col] != '1' && !visited[curPath.row+1][curPath.col]) {
                path np;
                np.row = curPath.row+1;
                np.col = curPath.col;
                np.dist = curPath.dist+1;
                visited[curPath.row+1][curPath.col] = true;
                bfs.push(np);
            }
            if (curPath.col > 0 && grid[curPath.row][curPath.col-1] != '1' && !visited[curPath.row][curPath.col-1]) {
                path np;
                np.row = curPath.row;
                np.col = curPath.col-1;
                np.dist = curPath.dist+1;
                visited[curPath.row][curPath.col-1] = true;
                bfs.push(np);
            }
        }
        cout << md << "\n";
        return 0;
    }
