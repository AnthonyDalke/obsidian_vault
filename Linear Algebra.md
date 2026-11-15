- Linear equations can contain any number of unknown values ($x$), as long as they remain in the first degree (power of 1)
	- Known values - coefficients - matrix becomes $n x m$

### Matrix Addition and Subtraction
- Both require matrices of same shapes
### Matrix Multiplication
- Matrices must take certain structures, with the count of rows in one matching the count of columns in the other, and vice-versa
	- Output becomes a matrix with a row count of the first matrix and a column count of the second matrix
	- Calculate by finding dot products of each row and column combination of the multiplied matrices
	- Example: multiplying two $2 x 3$ matrices would get evaluated as:
		- Row 1 from matrix A multiplied by column 1 from matrix B
		- Row 2 from matrix A multiplied by column 1 from matrix B
		- Row 1 from matrix A multiplied by column 2 from matrix B
		- Row 1 from matrix A multiplied by column 2 from matrix B

### Determinants and Matrix Transposition
- To calculate determinants by hand, recursively isolate smaller matrices within a larger matrix
	1. Select an index within the larger matrix ("pivot element")
	2. Eliminate the remaining items int he row and column of that item
	3. Compute the determinant of the remaining rows and columns
	4. Multiply that result by the item selected in step 1
	5. Repeat for the remaining pivot elements in the first row
	6. Add those results with alternating signs (i.e., add, subtract, add)
- Computation example, for a matrix Computation example, for a matrix $v = \begin{bmatrix} 0 \ 2 \ 4 \\ 6 \ 8 \ 10 \\ 12 \ 14 \ 16 \end{bmatrix}$
	- Index 1,1: $8 * 16 - 10 * 14 * 0 = (128 - 140) * 0 = 0$
	- Index 1,2: $6 * 16 - 10 * 12 * 2 = (96 - 120) * 2 = -48$
	- Index 1,3: $6 * 14 - 8 * 12 * 4 = (84 - 96) * 4 = -48$
	- Evaluates to: $0 - (-48) - 48 = 0$
- Matrix transposes entail swapping rows and columns
	- Column 1 becomes row 1, col. 2 -> row 2, etc.

### Diagonal Matrices
- For a $3 x 3$ matrix, the elements in indexes $[1, 1], [2, 2]$ and $[3, 3]$ comprise the "main diagonal"
	- To compute the trace of a main diagonal, sum these values
	- Traces can only exist in the square matrices
- Symmetric matrices have transposes equal to the original
- Multiplying any matrix by its transpose makes the result symmetric
- In diagonal matrices, all elements outside the main diagonal have values of 0
- In identity matrices, elements along the main diagonal all have values of 1
	- All identity matrices = diagonal matrices
	- Multiplying any matrix by an identity matrix results in the original matrix, like mulitplying a number by 1
- In zero matrices, all elements have values of 0

### Inverse Matrices
- Multiplying a matrix by its inverse with a dot product results in an identity matrix
- Conceptually, inverse matrices function like division

### Matrix Ranks
- Refer to the count of dimensions in matrices
	- e.g., $2 x 2$ matrix has a rank of 2

### Properties of Matrices
- They satisfy the commutative property of addition
	- i.e., ($a + b = b + a$)
- Associative property applies, as well
	- i.e., ($a + (b + c) = (a + b) + c$)
- The transpose of a transpose becomes the original matrix
- The transpose of two combined (added) matrices equals the sum of each's transpose
	- i.e., $(a + b).T = a.T + b.T$
- Similarly, the transpose of the dot product of two matrices equals the transpose of one and the dot product of the other transpose
	- i.e, $(a.dot(b)).T = (b.T).dot(a.T)$
- The transpose of a matrix multiplied by a scalar equals the scalar multiplied by the transpose of the matrix
	- i.e., $(r * a).T = r * a.T$