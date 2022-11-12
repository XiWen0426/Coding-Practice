**Approach 1: Set Up Boundaries (Best)** O(M\*N), O(1)
a. https://leetcode.com/submissions/detail/841148130/
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        int m = matrix.size(), n = matrix[0].size();
        for (int i = 0; i < (min(m, n) + 1) / 2; i++){
            for (int j = 0; j < n - 2 * i; j++)
                res.push_back(matrix[i][i + j]);
            for (int j = 0; j < m - 2 * i - 2; j++)
                res.push_back(matrix[i + 1 + j][n - 1 - i]);
            for (int j = 0; j < n - 2 * i; j++)
                res.push_back(matrix[m - 1 - i][n - 1 - i - j]);
            for (int j = 0; j < m - 2 * i - 2; j++)
                res.push_back(matrix[m - 2 - i - j][i]);
        }
        while (res.size() > m * n)
            res.pop_back();
        return res;
    }
};
```
b. https://leetcode.com/submissions/detail/841234497/
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        int m = matrix.size(), n = matrix[0].size();
        int l = 0, r = n - 1, top = 0, bot = m - 1;
        while (res.size() < m * n){
            for (int col = l; col <= r; col++)
                res.push_back(matrix[top][col]);
            for (int row = top + 1; row <= bot; row++)
                res.push_back(matrix[row][r]);
            if (top != bot){
                for (int col = r - 1; col >= l; col--)
                    res.push_back(matrix[bot][col]);
            }
            if (l != r){
                for (int row = bot - 1; row > top; row--)
                    res.push_back(matrix[row][l]);
            }
            l++;
            r--;
            top++;
            bot--;
        }
        return res;
    }
};
```
**Approach 2: Mark Visited Elements (Best)** O(M\*N), O(1)
https://leetcode.com/submissions/detail/841160622/
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        int m = matrix.size(), n = matrix[0].size();
        int dir[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        int d = 0;
        int row = 0, col = 0;
        int VISITED = 101;
        while (res.size() < m * n){
            res.push_back(matrix[row][col]);
            matrix[row][col] = VISITED;
            int next_row = row + dir[d][0];
            int next_col = col + dir[d][1];
            if (next_row < 0 || next_row >= m || next_col < 0 || next_col >= n || matrix[next_row][next_col] == 101)
                d = (d + 1) % 4;
            row += dir[d][0];
            col += dir[d][1];
        }
        return res;
    }
};
```
