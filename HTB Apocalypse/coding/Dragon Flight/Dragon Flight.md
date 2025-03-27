# Challenge
Dragon Flight

In the mystical realm of the Floating Isles, dragons soar between ancient sanctuaries. However, unpredictable wind conditions can either boost or hinder their journeys.

As a Dragon Flight Master, your mission is to:

- Handle both sudden wind changes and challenging flight path queries.
- Process update operations that modify the wind effect on any flight segment.
- Compute the maximum favorable continuous flight stretch (i.e., the maximum contiguous subarray sum) within a specified range.

Your precise calculations are critical to determine the safest and most efficient route for the dragons. Adapt quickly as wind conditions change, ensuring their journey remains uninterrupted.

## Input Format Explanation

The input provided to the challenge is structured as follows:

- **First Line:** Two space-separated integers, _N_ and _Q_.
    - _N_ represents the number of flight segments.
    - _Q_ represents the number of operations to perform.
- **Second Line:** _N_ space-separated integers representing the initial net wind effects for each flight segment.
    - A **positive** value indicates a tailwind, which helps the dragon travel further.
    - A **negative** value indicates a headwind, which reduces the effective flight distance.
- **Next Q Lines:** Each line represents an operation that can be one of the following:
    - `U i x`: An **update** operation where the wind effect on the _i_-th segment is changed to _x_.
    - `Q l r`: A **query** operation requesting the maximum contiguous subarray sum (i.e., the maximum net flight distance) for the segments in the range from _l_ to _r_ (inclusive).

## Flight Example

### Flight Path Input

6 6 -10 -7 -1 -4 0 -5 Q 3 3 U 2 9 Q 6 6 U 1 -1 Q 6 6 U 5 -9

### Expected Output

-1 -5 -5

### Explanation

 Step-by-Step Breakdown: 
 1. Initial Array: [-10, -7, -1, -4, 0, -5] - This array represents the wind effects for 6 flight segments. - Negative numbers indicate headwinds (reducing flight distance).
 2. Operation 1: Q 3 3 - Instruction: Query the subarray from index 3 to 
 3. - 1-indexed index 3 corresponds to the third element. - Extracted Subarray: [-1] - Maximum Contiguous Subarray Sum: Since there is only one element, the maximum sum is simply that element, -1. => Output: -1 3. Operation 2: U 2 9 - Instruction: Update the element at index 2 to 9. - 1-indexed index 2 refers to the second element, which was originally -7. - Array Change: Replace -7 with 9. - New Array becomes: [-10, 9, -1, -4, 0, -5] - Note: Update operations do not produce any output.
 4. Operation 3: Q 6 6 - Instruction: Query the subarray from index 6 to 6. - 1-indexed index 6 corresponds to the sixth element. - Extracted Subarray: [-5] - Maximum Contiguous Subarray Sum: With only one element (-5), the result is -5. => Output: -5 
 5. Operation 4: U 1 -1 - Instruction: Update the element at index 1 to -1. - 1-indexed index 1 refers to the first element, which was originally -10. - Array Change: Replace -10 with -1. - New Array becomes: [-1, 9, -1, -4, 0, -5] - Again, no output is produced for an update. 
 6. Operation 5: Q 6 6 - Instruction: Query the subarray from index 6 to 6 again. - The sixth element is still -5. - Extracted Subarray: [-5] - Maximum Contiguous Subarray Sum remains -5. => Output: -5 
 7. Operation 6: U 5 -9 - Instruction: Update the element at index 5 to -9. - 1-indexed index 5 refers to the fifth element, which was originally 0. - Array Change: Replace 0 with -9. - Final Array becomes: [-1, 9, -1, -4, -9, -5] - This operation is an update, so no output is generated.

```python
import sys

class SegmentTree:
    def __init__(self, arr):
        self.n = len(arr)
        self.tree = [None] * (4 * self.n)  # Segment tree structure
        self.build(arr, 0, 0, self.n - 1)

    def merge(self, left, right):
        """Merges two segment tree nodes."""
        if left is None:
            return right
        if right is None:
            return left
        
        total = left['total'] + right['total']
        max_prefix = max(left['max_prefix'], left['total'] + right['max_prefix'])
        max_suffix = max(right['max_suffix'], right['total'] + left['max_suffix'])
        max_subarray = max(left['max_subarray'], right['max_subarray'], left['max_suffix'] + right['max_prefix'])
        
        return {
            'total': total,
            'max_prefix': max_prefix,
            'max_suffix': max_suffix,
            'max_subarray': max_subarray
        }

    def build(self, arr, node, start, end):
        """Builds the segment tree."""
        if start == end:
            val = arr[start]
            self.tree[node] = {
                'total': val,
                'max_prefix': val,
                'max_suffix': val,
                'max_subarray': val
            }
        else:
            mid = (start + end) // 2
            left_child = 2 * node + 1
            right_child = 2 * node + 2
            
            self.build(arr, left_child, start, mid)
            self.build(arr, right_child, mid + 1, end)
            
            self.tree[node] = self.merge(self.tree[left_child], self.tree[right_child])

    def update(self, idx, val, node, start, end):
        """Updates a value at index idx."""
        if start == end:
            self.tree[node] = {
                'total': val,
                'max_prefix': val,
                'max_suffix': val,
                'max_subarray': val
            }
        else:
            mid = (start + end) // 2
            left_child = 2 * node + 1
            right_child = 2 * node + 2
            
            if idx <= mid:
                self.update(idx, val, left_child, start, mid)
            else:
                self.update(idx, val, right_child, mid + 1, end)
            
            self.tree[node] = self.merge(self.tree[left_child], self.tree[right_child])

    def query(self, l, r, node, start, end):
        """Queries the maximum subarray sum in range [l, r]."""
        if r < start or l > end:  # Out of range
            return None
        if l <= start and end <= r:  # Fully inside range
            return self.tree[node]
        
        mid = (start + end) // 2
        left_child = self.query(l, r, 2 * node + 1, start, mid)
        right_child = self.query(l, r, 2 * node + 2, mid + 1, end)
        
        return self.merge(left_child, right_child)

# Read input
n, q = map(int, sys.stdin.readline().split())
arr = list(map(int, sys.stdin.readline().split()))
tree = SegmentTree(arr)

# Process operations
for _ in range(q):
    op = sys.stdin.readline().split()
    if op[0] == 'U':  # Update operation
        i, x = int(op[1]) - 1, int(op[2])  # Convert 1-based index to 0-based
        tree.update(i, x, 0, 0, n - 1)
    elif op[0] == 'Q':  # Query operation
        l, r = int(op[1]) - 1, int(op[2]) - 1
        result = tree.query(l, r, 0, 0, n - 1)
        print(result['max_subarray'])

```

![](assets/Pasted%20image%2020250323103407.png)