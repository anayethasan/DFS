# DFS
BFS & DFS on a 2D Grid
In this learning session, I explored Depth-First Search (DFS) and Breadth-First Search (BFS) on a 2D grid. These traversal techniques help in exploring grids efficiently for different applications.

Depth-First Search (DFS) on a 2D Grid
DFS explores a grid by going as deep as possible along each direction before backtracking. It uses recursion and follows a stack-based approach.

Implementation of DFS
cpp
Copy
Edit
#include <bits/stdc++.h>
using namespace std;

char grid[105][105];
bool visited[105][105];
vector<pair<int, int>> d = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}}; // Directions

int n, m;

bool valid(int i, int j) {
    return (i >= 0 && i < n && j >= 0 && j < m);
}

void dfs(int si, int sj) {
    cout << si << " " << sj << endl;
    visited[si][sj] = true;

    for (int i = 0; i < 4; i++) {
        int ci = si + d[i].first;
        int cj = sj + d[i].second;

        if (valid(ci, cj) && !visited[ci][cj]) {
            dfs(ci, cj);
        }
    }
}

int main() {
    cin >> n >> m;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cin >> grid[i][j];
        }
    }

    int si, sj;
    cin >> si >> sj;

    memset(visited, false, sizeof(visited));
    dfs(si, sj);

    return 0;
}
Breadth-First Search (BFS) on a 2D Grid
BFS explores a grid level by level, ensuring that all nodes at a given depth are visited before moving deeper. It uses a queue-based approach.

Implementation of BFS
cpp
Copy
Edit
#include <bits/stdc++.h>
using namespace std;

char grid[105][105];
bool visited[105][105];
int level[105][105];
vector<pair<int, int>> d = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}}; // Directions

int n, m;

bool valid(int i, int j) {
    return (i >= 0 && i < n && j >= 0 && j < m);
}

void bfs(int si, int sj) {
    queue<pair<int, int>> q;
    q.push({si, sj});
    visited[si][sj] = true;
    level[si][sj] = 0;

    while (!q.empty()) {
        pair<int, int> par = q.front();
        q.pop();

        int par_i = par.first;
        int par_j = par.second;

        cout << par_i << " " << par_j << endl;

        for (int i = 0; i < 4; i++) {
            int ci = par_i + d[i].first;
            int cj = par_j + d[i].second;
            if (valid(ci, cj) && !visited[ci][cj]) {
                q.push({ci, cj});
                visited[ci][cj] = true;
                level[ci][cj] = level[par_i][par_j] + 1;
            }
        }
    }
}

int main() {
    cin >> n >> m;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cin >> grid[i][j];
        }
    }

    int si, sj, di, dj;
    cin >> si >> sj >> di >> dj;

    memset(visited, false, sizeof(visited));
    memset(level, -1, sizeof(level));
    bfs(si, sj);

    cout << level[di][dj] << endl;

    return 0;
}
Key Learnings
DFS (Depth-First Search)

Uses recursion and explores as deep as possible before backtracking.
Suitable for solving maze problems, connected components, and island counting.
BFS (Breadth-First Search)

Uses a queue and explores level by level.
Ideal for finding the shortest path in an unweighted graph or spreading processes like fire or water.
2D Grid Exploration

Represented using a matrix with cells acting as nodes.
Can be traversed in four directions (Up, Down, Left, Right).
Applications

Pathfinding algorithms (Shortest path in a maze).
Connected components in a grid (Counting islands).
Graph traversal for game development and simulations.
