# Challenge
ClockWork Gurdian

The Clockwork Sentinels defending Eldoria’s Skywatch Spire have gone rogue! You must navigate the spire, avoiding hostile sentinels and finding the safest path.

The Clockwork Sentinels defending Eldoria's Skywatch Spire have gone rogue! You must navigate through the spire, avoiding hostile sentinels and finding the safest path to the exit.

Write an algorithm to find the shortest safe path from the start position (0,0) to the exit ('E'), avoiding the sentinels (`1`).

## Example

### Example Grid and Output

```

[
    [0, 0, 1, 0, 0, 1],
    [0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0],
    [0, 0, 1, 1, 0, 'E']
]
```

**Output: 8**

**Step-by-Step Visualization:**  
  
**Step 0 (Start):**

Row 0: S   0   X   0   0   X
Row 1: 0   0   0   0   0   0
Row 2: 0   0   0   0   0   0
Row 3: 0   0   X   X   0   E
    

**Step 1:**

Row 0: S   1   X   0   0   X
Row 1: 0   0   0   0   0   0
Row 2: 0   0   0   0   0   0
Row 3: 0   0   X   X   0   E
    

**Step 2:**

Row 0: S   1   X   0   0   X
Row 1: 0   2   0   0   0   0
Row 2: 0   0   0   0   0   0
Row 3: 0   0   X   X   0   E
    

**Step 3:**

Row 0: S   1   X   0   0   X
Row 1: 0   2   3   0   0   0
Row 2: 0   0   0   0   0   0
Row 3: 0   0   X   X   0   E
    

**Step 4:**

Row 0: S   1   X   0   0   X
Row 1: 0   2   3   4   0   0
Row 2: 0   0   0   0   0   0
Row 3: 0   0   X   X   0   E
    

**Step 5:**

Row 0: S   1   X   0   0   X
Row 1: 0   2   3   4   5   0
Row 2: 0   0   0   0   0   0
Row 3: 0   0   X   X   0   E
    

**Step 6:**

Row 0: S   1   X   0   0   X
Row 1: 0   2   3   4   5   6
Row 2: 0   0   0   0   0   0
Row 3: 0   0   X   X   0   E
                          

**Step 7:**

Row 0: S   1   X   0   0   X
Row 1: 0   2   3   4   5   6
Row 2: 0   0   0   0   0   7
Row 3: 0   0   X   X   0   E
                          

**Step 8 (Exit reached):**

Row 0: S   1   X   0   0   X
Row 1: 0   2   3   4   5   6
Row 2: 0   0   0   0   0   7
Row 3: 0   0   X   X   0   E
                          

  

**Path Length: 8**

```python
import ast
from collections import deque

def shortest_safe_path(grid):
    rows, cols = len(grid), len(grid[0])
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]  # Right, Down, Left, Up
    
    # Find the exit position
    exit_pos = None
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 'E':
                exit_pos = (r, c)
    
    if not exit_pos:
        return -1  # No exit found
    
    queue = deque([(0, 0, 0)])  # (row, col, distance)
    visited = set()
    visited.add((0, 0))
    
    while queue:
        r, c, dist = queue.popleft()
        
        # If we reached the exit, return the distance
        if (r, c) == exit_pos:
            return dist
        
        # Explore all possible movements
        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and (nr, nc) not in visited:
                if grid[nr][nc] != 1:  # Not a sentinel
                    queue.append((nr, nc, dist + 1))
                    visited.add((nr, nc))
    
    return -1  # If no path exists

# Read input and convert string to list
input_text = input()
grid = ast.literal_eval(input_text)  # Convert string input to list

# Call function and print result
print(shortest_safe_path(grid))

```

![[HTB Apocalypse/coding/ClockWork Gurdian/assets/Pasted image 20250323104641.png]]