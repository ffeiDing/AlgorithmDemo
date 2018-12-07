```c
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        int m = triangle[n-1].size();
        int sum[n][m];
        fill(sum[0], sum[0]+n*m, 100010);
        sum[0][0] = triangle[0][0];
        for (int i = 1; i < n; i++){
            for (int j = 0; j < triangle[i].size(); j++){
                if (j-1 >= 0)
                    sum[i][j] = min(sum[i-1][j]+triangle[i][j], sum[i-1][j-1]+triangle[i][j]);
                else
                    sum[i][j] = sum[i-1][j]+triangle[i][j];
            }
        }
        int minres = 100010;
        for (int i = 0; i < m; i++)
            minres = min(minres, sum[n-1][i]);
        return minres;
    }
};
```
