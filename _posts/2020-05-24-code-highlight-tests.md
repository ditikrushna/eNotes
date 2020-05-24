---
layout: post
title: "CPC Test NITT (Temp. Post)"
categories: misc
author: "Ditikrushna Giri"
---


## Cake_Event___ 
    #include<bits/stdc++.h>
    using namespace std;
    typedef long long int lli;
    int main()
    {
         lli n,k,t;
         cin>>n>>k;
         vector<lli> a;lli sum=0;
         a.push_back(0);
         for(int i=1;i<=n;i++)
         {
             cin>>t;
             sum+=t;
             a.push_back(sum);
         }
         lli max=a[k]-a[0];
         for(lli i=0;i<=n-k;i++)
         {
             if(a[i+k]-a[i]>max)
             {
                 max=a[k+i]-a[i];
             }
         }
         cout<<max;
         return 0;
    } 



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
