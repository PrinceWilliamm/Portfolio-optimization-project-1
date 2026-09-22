### Take for example matrix A and B; ###
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 3 & 2 & 1 \end{bmatrix}, \quad B = \begin{bmatrix} 0 & 2 \\ 1 & -1 \\ 0 & 1 \end{bmatrix}$$
From there we obtain that AB equals with a step by step calculation;
1. **Top-Left Entry (Row 1 of $A$, Column 1 of $B$):**$$(1)(0) + (2)(1) + (3)(0) = 0 + 2 + 0 = \mathbf{2}$$
2. **Top-Right Entry (Row 1 of $A$, Column 2 of $B$):**$$(1)(2) + (2)(-1) + (3)(1) = 2 - 2 + 3 = \mathbf{3}$$
3. **Bottom-Left Entry (Row 2 of $A$, Column 1 of $B$):**
    $$(3)(0) + (2)(1) + (1)(0) = 0 + 2 + 0 = \mathbf{2}$$
4. **Bottom-Right Entry (Row 2 of $A$, Column 2 of $B$):**$$(3)(2) + (2)(-1) + (1)(1) = 6 - 2 + 1 = \mathbf{5}$$
	 Finally,
$$AB = \begin{bmatrix} 2 & 3 \\ 2 & 5 \end{bmatrix}$$
and that BA computes to a 3x3 matrix and equals after careful step by step calculation to;
$$BA = \begin{bmatrix} 0(1) + 2(3) & 0(2) + 2(2) & 0(3) + 2(1) \\ 1(1) + (-1)(3) & 1(2) + (-1)(2) & 1(3) + (-1)(1) \\ 0(1) + 1(3) & 0(2) + 1(2) & 0(3) + 1(1) \end{bmatrix}$$

5. **Row 1 calculations:**
    
    - $(0)(1) + (2)(3) = \mathbf{6}$
        
    - $(0)(2) + (2)(2) = \mathbf{4}$
        
    - $(0)(3) + (2)(1) = \mathbf{2}$
        
6. **Row 2 calculations:**
    
    - $(1)(1) + (-1)(3) = 1 - 3 = \mathbf{-2}$
        
    - $(1)(2) + (-1)(2) = 2 - 2 = \mathbf{0}$
        
    - $(1)(3) + (-1)(1) = 3 - 1 = \mathbf{2}$
        
7. **Row 3 calculations:**
    
    - $(0)(1) + (1)(3) = \mathbf{3}$
        
    - $(0)(2) + (1)(2) = \mathbf{2}$
        
    - $(0)(3) + (1)(1) = \mathbf{1}$
    Finally;
        $$BA = \begin{bmatrix} 6 & 4 & 2 \\ -2 & 0 & 2 \\ 3 & 2 & 1 \end{bmatrix}$$