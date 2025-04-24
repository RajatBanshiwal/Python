
# 🧩 Sudoku Solver

This Python program solves a standard 9x9 Sudoku puzzle using a **backtracking algorithm**.  
The puzzle is represented as a 2D list, where empty cells are denoted by `'.'`.

---

## 📜 Problem Statement

A Sudoku solution must satisfy the following rules:

- Each of the digits `1-9` must appear **exactly once in each row**.
- Each of the digits `1-9` must appear **exactly once in each column**.
- Each of the digits `1-9` must appear **exactly once in each of the 9 3x3 sub-boxes** of the grid.

The input puzzle may only have **one valid solution**.

---

## ✅ Example



### Input

```
python board = [
    ["5","3",".",".","7",".",".",".","."],
    ["6",".",".","1","9","5",".",".","."],
    [".","9","8",".",".",".",".","6","."],
    ["8",".",".",".","6",".",".",".","3"],
    ["4",".",".","8",".","3",".",".","1"],
    ["7",".",".",".","2",".",".",".","6"],
    [".","6",".",".",".",".","2","8","."],
    [".",".",".","4","1","9",".",".","5"],
    [".",".",".",".","8",".",".","7","9"]   ]
```

### Output
```

[
    ["5","3","4","6","7","8","9","1","2"],
    ["6","7","2","1","9","5","3","4","8"],
    ["1","9","8","3","4","2","5","6","7"],
    ["8","5","9","7","6","1","4","2","3"],
    ["4","2","6","8","5","3","7","9","1"],
    ["7","1","3","9","2","4","8","5","6"],
    ["9","6","1","5","3","7","2","8","4"],
    ["2","8","7","4","1","9","6","3","5"],
    ["3","4","5","2","8","6","1","7","9"]
]

```

## 💡 How It Works

The solution uses backtracking to fill in the grid:

1. Find the next empty cell.

2. Try placing digits '1' to '9'.

3. Check if the digit is valid (row, column, box).

4. If valid, recurse. If not, backtrack and try another digit.

5. Continue until the board is solved.

   ---

## 🧠  Implementation



```

class Solution(object):
    def solveSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: None Do not return anything, modify board in-place instead.
        """

        def is_valid(row, col, num):
            # Check row and column
            for i in range(9):
                if board[row][i] == num or board[i][col] == num:
                    return False
            
            # Check 3x3 box
            start_row, start_col = 3 * (row // 3), 3 * (col // 3)
            for i in range(3):
                for j in range(3):
                    if board[start_row + i][start_col + j] == num:
                        return False
            
            return True

        def backtrack():
            for row in range(9):
                for col in range(9):
                    if board[row][col] == '.':
                        for num in '123456789':
                            if is_valid(row, col, num):
                                board[row][col] = num
                                if backtrack():
                                    return True
                                board[row][col] = '.'  # backtrack
                        return False  # no valid number found
            return True  # all cells filled

        backtrack()

```


## 🚀 Usage

```
board = [
    ["5","3",".",".","7",".",".",".","."],
    ["6",".",".","1","9","5",".",".","."],
    [".","9","8",".",".",".",".","6","."],
    ["8",".",".",".","6",".",".",".","3"],
    ["4",".",".","8",".","3",".",".","1"],
    ["7",".",".",".","2",".",".",".","6"],
    [".","6",".",".",".",".","2","8","."],
    [".",".",".","4","1","9",".",".","5"],
    [".",".",".",".","8",".",".","7","9"]
]

Solution().solveSudoku(board)
print(board)

```
##  How to Run
python3 sudoku_solver.py


## 📎 License

This project is open-source and available under the MIT License.







