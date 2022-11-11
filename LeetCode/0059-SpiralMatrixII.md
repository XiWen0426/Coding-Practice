**Approach 1 - Traverse Layer by Layer in Spiral Form (Best)** O(n^2), O(1)

https://leetcode.com/submissions/detail/841048333/
```
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n, -1));
        int num = 1;
        for (int i = 0; i < n / 2; i++){
            for (int j = 0; j < n - 2 * i - 1; j++)
                res[i][i + j] = num++;
            for (int j = 0; j < n - 2 * i - 1; j++)
                res[i + j][n - 1 - i] = num++;
            for (int j = 0; j < n - 2 * i - 1; j++)
                res[n - 1 - i][n - 1 - i - j] = num++;
            for (int j = 0; j < n - 2 * i - 1; j++)
                res[n - 1 - i - j][i] = num++;
        }
        if (n % 2 == 1)
            res[n / 2][n / 2] = num++;
        return res;
    }
};
```
**Approach 2 - Optimized spiral traversal** O(n^2), O(1)

https://leetcode.com/submissions/detail/841085639/
```
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n, -1));
        int num = 1;
        int dir[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        int d = 0;
        int row = 0, col = 0;
        while (num <= n * n){
            res[row][col] = num++;
            int next_row = row + dir[d][0];
            int next_col = col + dir[d][1];
            if (next_row < 0 || next_row >= n || next_col < 0 || next_col >= n || res[next_row][next_col] != -1)
                d = (d + 1) % 4;
            row += dir[d][0];
            col += dir[d][1];
        }
        return res;
    }
};
```
