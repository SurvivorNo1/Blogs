# 回溯(Backtracking)

## Introduction

回溯（Backtracking）是一种解决问题的算法思想，通常用于解决组合、排列、子集和搜索等问题。它通过递归地尝试所有可能的选择，然后回溯到上一步继续尝试其他选择，直到找到问题的解或确定无解。

回溯算法的一般步骤如下：

1. **选择**：从问题的选择列表中选择一个选项。

2. **执行**：尝试选择，进入下一个步骤。

3. **回溯**：如果在当前选择下无法找到解，或者达到终止条件，回溯到上一步。

4. **撤销选择**：取消选择，尝试其他选择。

回溯通常适用于指数级别的问题，因为它会尝试所有可能的情况。回溯算法可以使用递归来实现，每次递归时传递参数，记录当前状态，然后在递归结束后恢复状态。

一个经典的回溯问题是排列问题，其中要求列出给定一组数的所有排列。以下是一个简单的排列问题的回溯算法示例：

```cpp
#include <iostream>
#include <vector>

void backtrack(std::vector<int>& nums, std::vector<int>& current, std::vector<bool>& used) {
    if (current.size() == nums.size()) {
        for (int num : current) {
            std::cout << num << " ";
        }
        std::cout << std::endl;
        return;
    }

    for (int i = 0; i < nums.size(); ++i) {
        if (!used[i]) {
            used[i] = true;
            current.push_back(nums[i]);
            backtrack(nums, current, used);
            current.pop_back();
            used[i] = false;
        }
    }
}

void generatePermutations(std::vector<int>& nums) {
    std::vector<int> current;
    std::vector<bool> used(nums.size(), false);
    backtrack(nums, current, used);
}

int main() {
    std::vector<int> nums = {1, 2, 3};
    generatePermutations(nums);
    return 0;
}
```

在这个示例中，`generatePermutations` 函数使用回溯来生成给定数字列表的所有排列。对于更复杂的问题，你可以根据问题的性质和约束设计相应的回溯算法。

## Problem

给定一个 `m x n` 二维字符网格 `board` 和一个字符串单词 `word` 。如果 `word` 存在于网格中，返回 `true` ；否则，返回 `false` 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

<img src="data:image/jpeg;base64,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">

 

**示例 1：**

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

**示例 2：**

```
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```

 

**提示：**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board `和` word `仅由大小写英文字母组成

##Solution (My Approach)

```c++

class Solution
{
public:
    bool isexist = 0;
    int m = 0;
    int len = 0;
    int n = 0;
    int **sign;
    string t;
    vector<vector<char> > map;
    void find(int i, int j, int cnt)
    {
        if (isexist)
        {
            return;
        }
        if (cnt == len)
        {
            isexist = true;
            return;
        }
        if (i >= 0 && j >= 0 && i < m && j < n)
        {
            if (map[i][j] == t[cnt]&&!sign[i][j])
            {
                cnt++;
                sign[i][j] = 1;
                if (cnt == len)
                {
                    isexist=1;
                }
                else
                {
                    find(i, j + 1, cnt);
                    find(i + 1, j, cnt);
                    find(i, j - 1, cnt);
                    find(i - 1, j, cnt);
                }
                sign[i][j] = 0;
            }
        }
    }

    bool exist(vector<vector<char> > &board, string word)
    {
        map = board;
        t = word;
        m = board.size();
        n = m > 0 ? board[0].size() : 0;
        len = word.size();
        sign = new int *[m];
        for (int i = 0; i < m; ++i)
        {
            sign[i] = new int[n]{0};
        }

        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (!isexist)
                {
                    find(i, j, 0);
                    cout << endl;
                }
                else
                {
                    break;
                }
            }
        }
        return isexist;
    }
};
```

