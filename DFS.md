
**DFS : Depth-First Search (深さ優先探索)**

Premise: 

		Input: double array
		Usage: Find the number of vertically, horizontally and diagnally connected
		group from given matrix 

Overall Process:
Prepare boolean double arrays to manage this algorithm boolean double array that has same width and height of original given double array that shows which node you have already visited. 

	1. Check if the surrounding nodes of given node has been visited && not out side of the array range.
	2. Check all the surrounding direction of given node with for loop of i < 8 (in case of 8 directions)
		(rowNbr[], colNbr[])
		(-1, -1) : Top Left 
		(-1, 0) :  Top
		(-1, 1) : Top Right
			and so on...
			

DFS Example (Java):
```java

	void DFS(int M[][], int row, int col, boolean visited[][])
	    {
	        // These arrays are used to get row and column numbers
	        // of 8 neighbors of a given cell
	        int rowNbr[] = new int[] { -1, 0, 0, 1 };
	        int colNbr[] = new int[] { 0, -1, 1, 0 };
	 
	        // Mark this cell as visited
	        visited[row][col] = true;
	 
	        // Recur for all connected neighbours
	        for (int k = 0; k < 4; ++k)
	            if (isSafe(M, row + rowNbr[k], col + colNbr[k], visited))
	                DFS(M, row + rowNbr[k], col + colNbr[k], visited);
	    }
    ```