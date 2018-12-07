```c
class Solution {
public:
    int n;
    int m;
    bool isValid(int x, int y){
        if (x >= 0 && y >= 0 && x < n && y < m)
            return true;
        return false;
    }
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        n = obstacleGrid.size();
        m = obstacleGrid[0].size();
        int vis[n][m], sum[n][m];
        memset(vis, 0, sizeof(vis));
        memset(sum, 0, sizeof(sum));
        sum[0][0] = 1-obstacleGrid[0][0];
        vis[0][0] = 1;
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (vis[i][j]==0 && obstacleGrid[i][j]==0){
                    if (isValid(i-1, j)){
                        if (obstacleGrid[i-1][j] == 0)
                            sum[i][j] += sum[i-1][j];
                    }
                    if (isValid(i+1, j)){
                        if (obstacleGrid[i+1][j] == 0)
                            sum[i][j] += sum[i+1][j];
                    }
                    if (isValid(i, j+1)){
                        if (obstacleGrid[i][j+1] == 0)
                            sum[i][j] += sum[i][j+1];
                    }
                    if (isValid(i, j-1)){
                        if (obstacleGrid[i][j-1] == 0)
                            sum[i][j] += sum[i][j-1];
                    }
                    vis[i][j] = 1;
                }
            }
        }
        return sum[n-1][m-1];
    }
};
```
