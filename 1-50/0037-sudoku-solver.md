# LeetCode 第 37 号问题：解数独

**难度困难**

### 题目描述
编写一个程序，通过填充空格来解决数独问题。
一个数独的解法需遵循如下规则：

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。
空白格用 '.' 表示。
![](/Animation/0037-sudoku-solver-1.png)
一个数独。
![](/Animation/0037-sudoku-solver-1.png)
答案被标成红色。

### 题目解析

## 一次迭代

### 代码实现

```php
//时间复杂度： O(1)
//空间复杂度： O(1)
class Solution
{

    /**
     * @param String[][] $board
     * @return Boolean
     */
    function isValidSudoku($board)
    {
        $row = $columns = $boxes = [];
        for ($i = 0; $i < 9; $i++) {
            for ($j = 0; $j < 9; $j++) {
                $num = $board[$i][$j];
                if ($num != '.') {
                    $box_index = floor($i / 3) * 3 + floor($j / 3);

                    if (++$row[$i][$num] > 1) {
                        echo 'row';
                        return false;
                    }
                    if (++$columns[$j][$num] > 1) {
                        echo 'columns';
                        return false;
                    }
                    if (++$boxes[$box_index][$num] > 1) {
                        echo 'boxes';

                        return false;
                    }
                }
            }
        }
        return true;
    }
}
```

