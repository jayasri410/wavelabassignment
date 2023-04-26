#include <iostream>
#include <bits/stdc++.h>

using namespace std;

int minTime(vector<vector<int>>& edges, int n, int k) {
        list<pair<int,int>> adj[n+1];
        for(auto edge: edges){
            adj[edge[0]].push_back({edge[1],edge[2]});
        }
        vector<int> dist(n+1,INT_MAX);
        priority_queue<pair<int,int>,vector<pair<int,int>>, greater<pair<int,int>>> pq;
        dist[k]=0;
        pq.push({dist[k],k});
        while(!pq.empty()){
            auto curr=pq.top();
            pq.pop();
            for(auto nei: adj[curr.second]){
                if(dist[nei.first]>nei.second+dist[curr.second]){
                    dist[nei.first]=dist[curr.second]+nei.second;
                    pq.push({dist[nei.first],nei.first});
                }
            }
        }
        int res=0;
        for(int i=1;i<=n;i++){
            res=max(res,dist[i]);
        }
        return res==INT_MAX ? -1 : res;
    }
    
int main(){
    
    int n,k;
    
    cin>>n>>k;
    vector<vector<int>> edges(n,vector<int>(n,0));
    for(int i=0;i<n;i++){
        int a,b,c;
        cin>>a>>b>>c;
        vector<int> temp;
        temp.push_back(a);
         temp.push_back(b);
          temp.push_back(c);
          edges.push_back(temp);
        
    }
    cout<<minTime(edges,n,k);
}
