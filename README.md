# DSA-Notes
Revision
# Graph 
   # Topological Sort 
         Question for Practise
            1. Course Schedule 1
            2. Course Schedule 2
            # Code Implementation 
            class Solution {
    public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        // calculate number of indegree of each node.....
        vector<int> indegree(numCourses, 0);
        vector<vector<int>> adj(numCourses);
        for (int i = 0; i < numCourses; i++) {
            for (auto& x : prerequisites) {
                int course = x[0];
                int pre = x[1];
                adj[pre].push_back(course);
                indegree[course]++;
            }
        }
        queue<int> q;
        vector<int> ans;
        // Push all nodes which has indegree zero
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                q.push(i);
            }
        }
        // BFS
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            ans.push_back(node);
            for (int& x : adj[node]) {
                indegree[x]--;
                if (indegree[x] == 0) {
                    q.push(x);
                }
            }
        }
        int n = ans.size();
        if (n == numCourses) {
            return ans;
        } else {
            return {};
        }
    }
};
            
