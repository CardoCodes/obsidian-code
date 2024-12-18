
### Approach

I start by finding the simplest approach in this case looking for a brute force method, additionally i can use the .sort() function to simply this brute force approach. I can then iterate through the sorted vector and check if the current element is different than the precious one, iterating a counter if the current element is consecutive to the previous one. We can then iterate on this idea and convert the input vector into an unordered set, which will allow for O(1) lookup time, and removes duplicates. Then we can iterate through the set and check for a sequence.
	1. Brute force - iterate through the array and keep track of the longest consecutive string,
	2. Hash Set  - Create a hash set and check if num-1 is not in the set. This will ensure we only count each sequence one, and start from the smallest number to avoid redundant computations.


### Implementation Details
- **Data Structures Used**:
  - Primary data structure(s)
  - Auxiliary data structures

- **Key Operations**:
  1. First key step
  2. Second key step
  3. Additional important steps

### Code Template
```cpp

// Brute force algorithm with sort and sequence check
// Time Complexity: O(nlogn) where n is the size of the int vector
// Space Complexity: O(1) constant space since we only use the nums int vector and some spare ints to keep track of count.

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        int count = 1;
        int max_cons = 0;

        if (n == 0) return 0;

        sort(nums.begin(), nums.end()); // O(nlogn) time on this sort

        for(int i = 1; i < n; i++){
            if(nums[i] != nums[i-1]){
                if(nums[i] == nums[i - 1] + 1){
                    count++;
                } else {
                    max_cons = max(max_cons, count);
                    count = 1;
                }
            }
        }

        return max(max_cons, count);



        
    }
};
```

### Complexity Analysis
- **Time Complexity**: O(?)
  - Breakdown of time complexity
  - Explanation of how complexity is calculated

- **Space Complexity**: O(?)
  - Breakdown of space complexity
  - Explanation of additional space used

### Important Notes
- Key observations
- Potential pitfalls
- Common edge cases to consider

### Variations and Follow-up
- Alternative approaches
- Related problems
- Potential optimizations

### Learning Highlights
- Key algorithms/techniques demonstrated
- Important C++ operations or methods used
```

## Best Practices
1. Always analyze time and space complexity
2. Consider edge cases
3. Use appropriate data structures
4. Write clean, readable code

