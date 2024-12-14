### Approach
One of the best methods to algorithm problems is to first think about the brute force approach. and then iterate on that idea to find other more optimized methods
	1. Brute Force - Solve this problem using a nested loop
	2. Dynamic Programming -  two pass strategy to calculate left and right products

### Implementation Details
- **Data Structures Used**:
  - The solution uses a two-pass strategy
	  - First pass (left-to-right): Compute prefix products
	  - Second pass (right-to-left): Incorporate suffix products
  - This approach is essentially computing: For each index `i`: `(Product of all elements left of i) * (Product of all elements right of i)`

- **Key Operations**:
  1. Prefix Pass
  2. Postfix Pass
  3. Array manipulation

### Code Template
```cpp
// Burte force algorithm with nested loop
// Time Complexity: O(n^2) Where N is the size of the nums array.
// Space Complexity: O(1) Constant space, excluding output array.

class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans;

        for(int i = 0; i < n; i++){
            int product = 1;
            for(int j = 0; j < n; j++){
                if (i == j) continue;
                product *= nums[j];
            }
            ans.push_back(product);
        }
        return ans;
    }
};


// Dynamic Programming with space optimization 
// Time Complexity: O(N) Where N is the size of the nums array
// Space Complexity: O(1) Using only the output array and single variable `right`
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n);

        ans[0] = 1;
        for(int i = 1; i < n; i++){
            ans[i] = ans[i - 1] * nums[i - 1];
        }

        int right = 1;
        for(int i = n - 1; i >= 0; i--){
            ans[i] *= right;
            right *= nums[i];
        }
        
        return ans;
    }
};


```

### Complexity Analysis
- **Time Complexity**: O(N)
  - Where N is the size of the nums array. Two linear passes through the array.

- **Space Complexity**: O(1)
  - Using only the output array and a single variable `right`

### Important Notes
- Categorized as a "Prefix/Suffix Product" algorithm
- Demonstrates in-place modification technique
- Avoids division, which can be problematic with zero values

### Variations and Follow-up
- Can be adapted to handle arrays with zero values
- Can be modified to compute more complex cumulative transformations


