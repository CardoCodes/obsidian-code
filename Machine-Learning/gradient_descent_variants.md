### Approach

Gradient descent is an iterative optimization algorithm used to minimize a cost function by updating parameters in the direction of steepest descent. We'll implement three variants: batch, stochastic, and mini-batch gradient descent, each with different trade-offs between computational efficiency and convergence stability.

### Implementation Details

- Algorithms Used
    - Batch Gradient Descent
        - $\theta_j = \theta_j - \alpha \centerdot \nabla J(\theta)$
        - Update once per iteration using all samples: 
	        - $w_{t+1} = w_t - \alpha\frac{1}{n}\sum_{i=1}^{n}x_i(\hat{y}_i - y_i)$ 
	        - $b_{t+1} = b_t - \alpha\frac{1}{n}\sum_{i=1}^{n}(\hat{y}_i - y_i)$
        - Updates parameters using the gradient computed over the entire dataset
        - Most stable but computationally expensive for large datasets
    - Stochastic Gradient Descent (SGD)
        - $\theta_j = \theta_j - \alpha \centerdot \nabla J_i(\theta)$
        - Update for each sample $i$: 
	        - $w_{t+1} = w_t - \alpha x_i(\hat{y}_i - y_i)$
	        - $b_{t+1} = b_t - \alpha(\hat{y}_i - y_i)$
        - Updates parameters using gradient computed from a single random example
        - Faster but noisier convergence
    - Mini Batch Gradient Descent
        - $\theta_j = \theta_j - \alpha \centerdot \nabla J_B(\theta)$
        - Update for each mini-batch $B$ of size $m$: 
	        - $w_{t+1} = w_t - \alpha\frac{1}{m}\sum_{i\in B}x_i(\hat{y}_i - y_i)$ 
	        - $b_{t+1} = b_t - \alpha\frac{1}{m}\sum_{i\in B}(\hat{y}_i - y_i)$
        - Updates parameters using gradient computed from a subset of examples
        - Balances stability and computational efficiency
- **Key Operations**:
    1. Data Preparation: Normalize features and initialize weights
    2. Forward Pass: Compute predictions using current weights
    3. Error Calculation: Calculate the difference between predictions and actual values
    4. Gradient Computation: Calculate the gradient based on the chosen method
    5. Weight Update: Adjust weights using the computed gradient and learning rate

### Code Template

```python
import numpy as np

def gradient_descent(X, y, weights, learning_rate, n_iterations, batch_size=32, method='batch'):
    m = len(y)
    cost_history = []
    
    for iteration in range(n_iterations):
        if method == 'batch':
            # Calculate the gradient using all data points
            predictions = X.dot(weights)
            errors = predictions - y
            gradient = 2 * X.T.dot(errors) / m
            weights = weights - learning_rate * gradient
            
            # Calculate cost for monitoring
            cost = np.mean(errors ** 2)
            cost_history.append(cost)
        
        elif method == 'stochastic':
            # Shuffle data for randomization
            indices = np.random.permutation(m)
            X_shuffled = X[indices]
            y_shuffled = y[indices]
            
            # Update weights for each data point individually
            for i in range(m):
                prediction = X_shuffled[i].dot(weights)
                error = prediction - y_shuffled[i]
                gradient = 2 * X_shuffled[i].T * error
                weights = weights - learning_rate * gradient
                
                if i % 100 == 0:  # Monitor cost less frequently
                    cost = np.mean((X.dot(weights) - y) ** 2)
                    cost_history.append(cost)
        
        elif method == 'mini_batch':
            # Shuffle data and create mini-batches
            indices = np.random.permutation(m)
            X_shuffled = X[indices]
            y_shuffled = y[indices]
            
            for i in range(0, m, batch_size):
                X_batch = X_shuffled[i:i+batch_size]
                y_batch = y_shuffled[i:i+batch_size]
                
                predictions = X_batch.dot(weights)
                errors = predictions - y_batch
                gradient = 2 * X_batch.T.dot(errors) / batch_size
                weights = weights - learning_rate * gradient
            
            # Calculate cost for monitoring
            cost = np.mean((X.dot(weights) - y) ** 2)
            cost_history.append(cost)
                
    return weights, cost_history
```

### Complexity Analysis

- **Time Complexity**:
    - Batch Gradient Descent: O(n_iterations * m * d)
        - m: number of examples
        - d: number of features
    - Stochastic Gradient Descent: O(n_iterations * m * d)
        - Faster in practice despite same theoretical complexity
    - Mini-batch Gradient Descent: O(n_iterations * m * d)
        - Intermediate performance between batch and SGD
- **Space Complexity**: O(d)
    - Weights vector: O(d)
    - Gradient vector: O(d)
    - Temporary computations: O(batch_size * d)
    - Additional space for cost history: O(n_iterations)

### Important Notes

- Learning rate selection is crucial for convergence
- Feature scaling is essential for optimal performance
- SGD requires shuffling data to avoid systematic biases
- Mini-batch size affects both stability and speed
- Monitor cost history to detect convergence issues
- Consider using adaptive learning rates for better convergence

### Learning Highlights

- Key algorithms/techniques demonstrated:
    - Different gradient descent variants
    - Vectorized operations with NumPy
    - Cost function monitoring
    - Batch processing
- Important Python operations:
    - NumPy array operations
    - Matrix multiplication (dot product)
    - Random permutation for shuffling
    - Array slicing for batch creation
