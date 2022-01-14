//# Prim-s-Algorithm-
#include<bits/stdc++.h>
using namespace std;
vector<int> prims(vector<pair<int,int>>adj[],int n){
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>pq;
    pq.push(make_pair(0,0));
    vector<int>key(n,INT_MAX),parent(n,-1);
    vector<bool>vis(n,false);
    key[0]=0;
    while(!pq.empty()){
        int x=pq.top().second;
        pq.pop();
        vis[x]=true;
        for(auto it:adj[x]){
            if(vis[it.first]==false && it.second<key[it.first]){
                parent[it.first]=x;
                key[it.first]=it.second;
                pq.push(make_pair(key[it.first],it.first));
            }
        }
    }
    return parent;
}
int main(){
    int t;
    cin>>t;
    while(t--){
        int n,m;
        cin>>n>>m;
        vector<pair<int,int>>adj[n];
        for(int i=0;i<m;i++) {
            int a,b,c;
            cin>>a>>b>>c;
            adj[a].push_back(make_pair(b,c));
            adj[b].push_back(make_pair(a,c));
        }
        vector<int>ans=prims(adj,n);
        for(int i=1;i<n;i++) cout<<i<<"->"<<ans[i]<<endl;
    }
}
