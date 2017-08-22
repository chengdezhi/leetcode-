# leetcode 329 Longest Increasing Path in a Matrix

    class Solution {
        private int m,n;
        private int[][] cached;
        private static final int[][] dirs = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        public int longestIncreasingPath(int[][] matrix) {
            if(matrix==null) return 0;
            if(matrix.length==0) return 0;
            m = matrix.length;
            n = matrix[0].length;
            cached = new int[m][n];
            int ans = 0;
            for(int i=0;i<m;i++){
                for(int j=0;j<n;j++){
                    ans = Math.max(ans, dfs(matrix, i, j));
                }
            }
            return ans;
        }

        private int dfs(int[][] matrix, int i, int j){
            // System.out.println(cached[i][j]);
            if(cached[i][j]!=0)  return cached[i][j];
            int ans = 0;
            for(int[] d: dirs){
                int n_i = i + d[0];
                int n_j = j + d[1];
                if(n_i>=0&&n_j>=0&&n_i<m&&n_j<n&&matrix[n_i][n_j]>matrix[i][j]){
                    cached[i][j] = Math.max(cached[i][j], dfs(matrix, n_i, n_j));
                }
            }
            return  ++cached[i][j];
        }
    
    }
