---
title: Word Search
---

### 描述

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where `"adjacent"` cells are those horizontally or vertically neighbouring. The same letter cell may not be used more than once.

For example,
Given board =

```
[
  ["ABCE"],
  ["SFCS"],
  ["ADEE"]
]
```

word = `"ABCCED"`, -> returns `true`,

word = `"SEE"`, -> returns `true`,

word = `"ABCB"`, -> returns `false`.

### 分析

无。

### 代码

import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

<Tabs
defaultValue="python"
values={[
{ label: 'Python', value: 'python', },
{ label: 'Java', value: 'java', },
{ label: 'C++', value: 'cpp', },
]
}>
<TabItem value="java">

```java
// Word Search
// 深搜，递归
// 时间复杂度O(n^2*m^2)，空间复杂度O(n^2)
public class Solution {
    public boolean exist(char[][] board, String word) {
        final int m = board.length;
        final int n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                if (dfs(board, word, 0, i, j, visited))
                    return true;
        return false;
    }
    private static boolean dfs(char[][] board, String word,
                    int index, int x, int y, boolean[][] visited) {
        if (index == word.length())
            return true; // 收敛条件

        if (x < 0 || y < 0 || x >= board.length || y >= board[0].length)
            return false;  // 越界，终止条件

        if (visited[x][y]) return false; // 已经访问过，剪枝

        if (board[x][y] != word.charAt(index)) return false; // 不相等，剪枝

        visited[x][y] = true;
        boolean ret = dfs(board, word, index + 1, x - 1, y, visited) || // 上
                dfs(board, word, index + 1, x + 1, y, visited)    || // 下
                dfs(board, word, index + 1, x, y - 1, visited)    || // 左
                dfs(board, word, index + 1, x, y + 1, visited);      // 右
        visited[x][y] = false;
        return ret;
    }
}
```

</TabItem>
<TabItem value="cpp">

```cpp
// Word Search
// 深搜，递归
// 时间复杂度O(n^2*m^2)，空间复杂度O(n^2)
class Solution {
public:
    bool exist(const vector<vector<char> > &board, const string& word) {
        const int m = board.size();
        const int n = board[0].size();
        vector<vector<bool> > visited(m, vector<bool>(n, false));
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                if (dfs(board, word, 0, i, j, visited))
                    return true;
        return false;
    }
private:
    static bool dfs(const vector<vector<char> > &board, const string &word,
            int index, int x, int y, vector<vector<bool> > &visited) {
        if (index == word.size())
            return true; // 收敛条件

        if (x < 0 || y < 0 || x >= board.size() || y >= board[0].size())
            return false;  // 越界，终止条件

        if (visited[x][y]) return false; // 已经访问过，剪枝

        if (board[x][y] != word[index]) return false; // 不相等，剪枝

        visited[x][y] = true;
        bool ret = dfs(board, word, index + 1, x - 1, y, visited) || // 上
                dfs(board, word, index + 1, x + 1, y, visited)    || // 下
                dfs(board, word, index + 1, x, y - 1, visited)    || // 左
                dfs(board, word, index + 1, x, y + 1, visited);      // 右
        visited[x][y] = false;
        return ret;
    }
};
```

</TabItem>

<TabItem value="python">

```python
# Word Search
# 深搜，递归
# 时间复杂度O(n^2*m^2)，空间复杂度O(n^2)
class Solution:
    def exist(self, board: list[list[str]], word: str) -> bool:
        m = len(board)
        n = len(board[0])
        visited = [[False] * n for _ in range(m)]
        for i in range(m):
            for j in range(n):
                if self.dfs(board, word, 0, i, j, visited):
                    return True
        return False

    def dfs(self, board: list[list[str]], word: str,
            index: int, x: int, y: int, visited: list[list[bool]]) -> bool:
        if index == len(word):
            return True  # 收敛条件

        if x < 0 or y < 0 or x >= len(board) or y >= len(board[0]):
            return False  # 越界，终止条件

        if visited[x][y]:
            return False  # 已经访问过，剪枝

        if board[x][y] != word[index]:
            return False  # 不相等，剪枝

        visited[x][y] = True
        ret = (self.dfs(board, word, index + 1, x - 1, y, visited) or  # 上
               self.dfs(board, word, index + 1, x + 1, y, visited) or  # 下
               self.dfs(board, word, index + 1, x, y - 1, visited) or  # 左
               self.dfs(board, word, index + 1, x, y + 1, visited))    # 右
        visited[x][y] = False
        return ret
```

</TabItem>
</Tabs>
