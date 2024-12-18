
### Approach

The problem requires finding the length of the longest consecutive sequence in an unsorted array. The key insights are:
1. Brute force approach involves sorting and checking consecutive elements, which is O(nlogn)
2. Optimize by using an unordered set for O(1) lookups
3. Identify the start of each sequence by checking if num-1 is not in the set
4. Count consecutive elements from each sequence start

The hash set approach allows us to:
- Remove duplicates efficiently
- Achieve O(n) time complexity
- Start counting sequences only from their smallest element
- Avoid redundant computations by checking sequence starts

### Implementation Details
-  **Data Structures Used**:
    - Primary data structure:
        - `unordered_set<int>`: Stores unique numbers for O(1) lookup
    - Auxiliary data structures:
        - Integer variables to track sequence length and longest sequence
- **Key Operations**:
    1. Convert input vector to an unordered set
    2. Iterate through each number in the set
    3. Check if the current number is the start of a sequence (no num-1 in set)
    4. If it's a sequence start, count consecutive elements
    5. Update the longest sequence length

### Code Template
```cpp

// Brute force algorithm with sort and sequence check
// Time Complexity: O(nlogn)
// Space Complexity: O(1)

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

// Time Complexity: O(n)
// Space Complexity: O(n)
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> numSet(nums.begin(), nums.end());
        int longest = 0;
        
        for (int num : numSet) {
            if (numSet.find(num - 1) == numSet.end()) {
                int length = 1;
                while (numSet.find(num + length) != numSet.end()) {
                    length++;
                }
                longest = max(longest, length);
            }
        }
        
        return longest;
    }
};
```

### Complexity Analysis
- **Time Complexity**: O(n)
    - Creating the unordered set takes O(n) time
    - Iterating through the set once takes O(n)
    - Inner while loop might seem nested, but each number is visited at most twice
    - Total time complexity remains O(n)
- **Space Complexity**: O(n)
    - Unordered set stores all unique numbers from the input
    - Additional constant space for tracking sequence length
    - Space directly proportional to the number of unique elements in the input
### Important Notes
- Handles empty input array
- Efficiently deals with duplicate numbers
- Only counts sequences starting from their smallest element
- Works with both positive and negative integers
- Key observation: checking num-1 absence ensures unique sequence counting
### Variations and Follow-up
- Alternative approaches:
    - Sorting-based solution (O(nlogn) time)
    - Disjoint set (Union-Find) approach
- Related problems:
    - Finding subsequences
    - Longest increasing subsequence
    - Maximum consecutive elements in an array
- Potential optimizations:
    - Early termination if no sequences found
    - Combine set creation and sequence checking in a single pass
### Learning Highlights
- Demonstrated efficient use of `unordered_set`
- Showcased O(n) time complexity algorithm
- C++ features utilized:
    - Range-based for loop
    - Set constructors
    - `max()` function
- Importance of choosing the right data structure

