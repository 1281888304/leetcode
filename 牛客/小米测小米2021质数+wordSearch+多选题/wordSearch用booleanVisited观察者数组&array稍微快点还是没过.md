

```` 
class Solution {
    int rows, cols;
    char[][] board;
    char[] word;
    int[][] next = new int[][]{{1, 0}, {0, 1}, {-1, 0}, {0, -1}};
    boolean[][] marked;
    public boolean exist(char[][] board, String word) {
        this.rows = board.length;
        this.cols = board[0].length;
        this.board = board;
        this.word = word.toCharArray();
        this.marked = new boolean[rows][cols];
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (search(0, row, col)) return true;
            }
        }
        return false;
    }
    private boolean search(int pos, int row, int col) {
        if (row < 0 || row >= rows || col < 0 || col >= cols || marked[row][col]) return false;
        
        if (board[row][col] != word[pos]) return false;
        
        if (pos == word.length - 1) return true;
        marked[row][col] = true;
        
        for (int[] nex : next) {
            if (search(pos + 1, row + nex[0], col + nex[1])) return true;
        }
        
        marked[row][col] = false;
        return false;
    }
}
````
