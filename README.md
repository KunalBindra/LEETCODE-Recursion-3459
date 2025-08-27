# LEETCODE-Recursion-3459
---

### 📌 Example Input

Let’s assume:

```java
int[][] grid = {
    {1, 2, 1},
    {2, 1, 2},
    {1, 2, 1}
};
```

* `m = 3`, `n = 3`
* Directions `dir`:

  * `0 → (1,1)`  (down-right)
  * `1 → (1,-1)` (down-left)
  * `2 → (-1,-1)` (up-left)
  * `3 → (-1,1)`  (up-right)

---

### 📌 Step 1: Initialization

* `t[m][n][4][2]` is filled with `-1`.
* `result = 0`.

---

### 📌 Step 2: Outer Loops in `lenOfVDiagonal`

We iterate all cells.

👉 At `(0,0)` → grid\[0]\[0] = **1** (condition passes)
We try all 4 directions from here.

---

### 📌 Step 3: First Solve Call

Call:

```java
solve(0, 0, d=0, CT=1, val=2, grid)
```

* We are at `(0,0)` with value `1`.
* We expect the next cell in diagonal (down-right) to be **2** (since we started with `val=2`).

---

### 📌 Step 4: Inside `solve(0,0,0,1,2,grid)`

* Compute `(i_, j_) = (0+1, 0+1) = (1,1)`
* `grid[1][1] = 1` ❌ but we wanted `val=2`.
* Condition fails ⇒ return `0`.

So from `(0,0)` in direction 0 → path length = `1+0 = 1`.

---

### 📌 Step 5: Next Direction

Call:

```java
solve(0,0,d=1,CT=1,val=2,grid)
```

* `(i_, j_) = (1, -1)` → out of bounds ⇒ returns `0`.

So length = `1`.

---

### 📌 Step 6: Try `(0,0,d=3,CT=1,val=2)`

* `(i_,j_) = (1,1)` again, value=1 (not 2) → fail.

So `(0,0)` contributes **max length = 1**.

---

### 📌 Step 7: Move to `(0,1)` (grid\[0]\[1] = 2)

We only start when grid\[i]\[j] == **1**, so skip.

---

### 📌 Step 8: Move to `(0,2)` → grid\[0]\[2] = 1

Try direction `d=0 (down-right)`:

* `(i_,j_) = (1,3)` out of bounds ⇒ return `0`.

Try direction `d=1 (down-left)`:

* `(i_,j_) = (1,1)` and grid\[1]\[1]=1, but we expected `2` ⇒ fail.

So still max=1.

---

### 📌 Step 9: More Interesting Case `(1,1)=1`

This is center of grid.

Check direction `d=0`:

* `(i_,j_) = (2,2)`, grid\[2]\[2]=1 but val=2 → fails.

Check direction `d=1`:

* `(i_,j_) = (2,0)`, grid\[2]\[0]=1 but val=2 → fails.

Check direction `d=3`:

* `(i_,j_) = (2,2)`, again 1 vs 2 → fails.

So again length=1.

---

### 📌 Step 10: Summary of Dry Run

For this grid:

```
1 2 1
2 1 2
1 2 1
```

The function would return `1`, because no alternating diagonal chain of `1-2-1-2...` exists longer than a single cell.

---

### 🔑 Key Observations from Dry Run

* Function starts **only at cells with value 1**.
* It looks diagonally for the next cell having **2**, then next should be **0**, then `2`, then `0`… (alternating).
* `CT=1` means you are allowed to **turn direction once**.
* Memoization (`t`) ensures no repeated recomputation.

---
