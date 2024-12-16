
### Approach

The problem requires validating a 9x9 Sudoku board by checking three key constraints:

1. Each row must contain digits 1-9 without repetition
2. Each column must contain digits 1-9 without repetition
3. Each of the nine 3x3 sub-boxes must contain digits 1-9 without repetition

The approach uses hash-based data structures to efficiently track unique digits in each row, column, and 3x3 square.
### Implementation Details
- ** Data Structures Used**:
    - Primary data structures:
        - `unordered_map<int, unordered_set<char>> rows`: Tracks unique digits in each row
        - `unordered_map<int, unordered_set<char>> cols`: Tracks unique digits in each column
        - `map<pair<int, int>, unordered_set<char>> squares`: Tracks unique digits in each 3x3 square
    - Auxiliary data structures:
        - `pair<int, int>`: Used as a key to identify 3x3 squares
        - `unordered_set<char>`: Ensures constant-time duplicate checking
- **Key Operations**:
    1. Iterate through each cell in the 9x9 board
    2. Skip empty cells (denoted by '.')
    3. Check for duplicates in corresponding row, column, and 3x3 square
    4. If no duplicates found, insert the digit into respective sets
    5. Return false if any duplicate is detected, true otherwise

### Code Template
```cpp

class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        for (int row = 0; row < 9; row++) {
            unordered_set<char> seen;
            for (int i = 0; i < 9; i++) {
                if (board[row][i] == '.') continue;
                if (seen.count(board[row][i])) return false;
                seen.insert(board[row][i]);
            }
        }
        
        for (int col = 0; col < 9; col++) {
            unordered_set<char> seen;
            for (int i = 0; i < 9; i++) {
                if (board[i][col] == '.') continue;
                if (seen.count(board[i][col])) return false;
                seen.insert(board[i][col]);
            }
        }
        
        for (int square = 0; square < 9; square++) {
            unordered_set<char> seen;
            for (int i = 0; i < 3; i++) {
                for (int j = 0; j < 3; j++) {
                    int row = (square / 3) * 3 + i;
                    int col = (square % 3) * 3 + j;
                    if (board[row][col] == '.') continue;
                    if (seen.count(board[row][col])) return false;
                    seen.insert(board[row][col]);
                }
            }
        }
        
        return true;
    }
};

class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        unordered_map<int, unordered_set<char>> rows, cols;
        map<pair<int, int>, unordered_set<char>> squares;

        for (int r = 0; r < 9; r++) {
            for (int c = 0; c < 9; c++) {
                if (board[r][c] == '.') continue;
                
                pair<int, int> squareKey = {r / 3, c / 3};

                if (rows[r].count(board[r][c]) || cols[c].count(board[r][c]) || squares[squareKey].count(board[r][c])) {
                    return false
                }

                rows[r].insert(board[r][c]);
                cols[c].insert(board[r][c]);
                squares[squareKey].insert(board[r][c]);
            }
        }
        return true;
    }
};
```

### Complexity Analysis
- **Time Complexity**: O(1)
    - Fixed board size of 9x9
    - Single pass through all 81 cells
    - Constant-time set operations (insert, count)
    - Despite nested loops, complexity remains O(1) due to fixed board dimensions
- **Space Complexity**: O(1)
    - Constant extra space used
    - Sets for rows, columns, and squares have a maximum size of 9
    - Space requirements do not grow with input size

### Important Notes
- Handles empty cells (marked with '.') gracefully
- Uses separate data structures for rows, columns, and squares
- Calculates 3x3 square coordinates using integer division and modulo
- Assumes input is a valid 9x9 character matrix

### Variations and Follow-up
- Alternative approaches:
    - Bit manipulation for more space-efficient tracking
    - Single-pass solution with combined checking
- Related problems:
    - Sudoku solver
    - Valid Sudoku generator
- Potential optimizations:
    - Early termination if invalid state detected
    - Potential bit vector implementation
### Learning Highlights
- Demonstrated use of hash-based data structures
- Efficient duplicate tracking with `unordered_set`
- Clever use of integer division for grid coordinate mapping
- C++ features: `unordered_map`, `unordered_set`, `pair`


