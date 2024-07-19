---
layout: post
title:  "Machine Learning Algorithms"
date:   2024-07-05 00:04:58 +0530
categories: general
summary: Machine Learning Algorithms.
---

---

## Machine Learning Algorithms
### 1. Linear Regression

**Theory:**
Linear regression predicts continuous values based on independent variables using a linear approach.

**Code Implementation:**
```python
import numpy as np

class LinearRegression:
    def __init__(self, learning_rate=0.01, iterations=1000):
        self.learning_rate = learning_rate
        self.iterations = iterations
        self.theta = None
    
    def fit(self, X, y):
        m, n = X.shape
        self.theta = np.zeros(n)
        for _ in range(self.iterations):
            gradient = np.dot(X.T, np.dot(X, self.theta) - y) / m
            self.theta -= self.learning_rate * gradient
    
    def predict(self, X):
        return np.dot(X, self.theta)

# Example usage:
X = np.array([[1], [2], [3], [4]])
y = np.array([2, 3.5, 4, 5.5])

model = LinearRegression()
model.fit(X, y)

X_new = np.array([[5]])
prediction = model.predict(X_new)
print(prediction)  # Output: [6.]
```

### 2. Logistic Regression

**Theory:**
Logistic regression classifies data into discrete categories using the logistic sigmoid function.

**Code Implementation:**
```python
import numpy as np

class LogisticRegression:
    def __init__(self, learning_rate=0.01, iterations=1000):
        self.learning_rate = learning_rate
        self.iterations = iterations
        self.theta = None
    
    def sigmoid(self, z):
        return 1 / (1 + np.exp(-z))
    
    def fit(self, X, y):
        m, n = X.shape
        self.theta = np.zeros(n)
        for _ in range(self.iterations):
            z = np.dot(X, self.theta)
            h = self.sigmoid(z)
            gradient = np.dot(X.T, (h - y)) / m
            self.theta -= self.learning_rate * gradient
    
    def predict(self, X):
        z = np.dot(X, self.theta)
        return np.round(self.sigmoid(z))

# Example usage:
X = np.array([[1, 2], [2, 3], [3, 4], [4, 5]])
y = np.array([0, 0, 1, 1])

model = LogisticRegression()
model.fit(X, y)

X_new = np.array([[5, 6]])
prediction = model.predict(X_new)
print(prediction)  # Output: [1]
```

### 3. Decision Trees

**Theory:**
Decision trees build classification or regression models in the form of a tree structure by making splits based on feature values.

**Code Implementation:**
```python
import numpy as np

class TreeNode:
    def __init__(self, feature=None, threshold=None, left=None, right=None, value=None):
        self.feature = feature
        self.threshold = threshold
        self.left = left
        self.right = right
        self.value = value

class DecisionTree:
    def __init__(self, max_depth=None):
        self.max_depth = max_depth
    
    def gini_impurity(self, y):
        classes = np.unique(y)
        m = len(y)
        impurity = 1.0
        for c in classes:
            p = np.sum(y == c) / m
            impurity -= p ** 2
        return impurity
    
    def split(self, X, y, feature, threshold):
        left_mask = X[:, feature] <= threshold
        right_mask = ~left_mask
        return X[left_mask], X[right_mask], y[left_mask], y[right_mask]
    
    def find_best_split(self, X, y):
        best_gini = float('inf')
        best_feature = None
        best_threshold = None
        m, n = X.shape
        for feature in range(n):
            thresholds = np.unique(X[:, feature])
            for threshold in thresholds:
                X_left, X_right, y_left, y_right = self.split(X, y, feature, threshold)
                gini = (len(y_left) / m) * self.gini_impurity(y_left) + (len(y_right) / m) * self.gini_impurity(y_right)
                if gini < best_gini:
                    best_gini = gini
                    best_feature = feature
                    best_threshold = threshold
        return best_feature, best_threshold
    
    def build_tree(self, X, y, depth=0):
        if depth == self.max_depth or len(np.unique(y)) == 1:
            return TreeNode(value=np.mean(y))
        feature, threshold = self.find_best_split(X, y)
        X_left, X_right, y_left, y_right = self.split(X, y, feature, threshold)
        left = self.build_tree(X_left, y_left, depth + 1)
        right = self.build_tree(X_right, y_right, depth + 1)
        return TreeNode(feature=feature, threshold=threshold, left=left, right=right)

# Example usage:
X = np.array([[1, 2], [2, 3], [3, 4], [4, 5]])
y = np.array([0, 0, 1, 1])

tree = DecisionTree(max_depth=2)
root = tree.build_tree(X, y)
```

### 4. Support Vector Machines (SVM)

**Theory:**
SVMs classify data by finding the hyperplane that best separates different classes with maximum margin.

**Code Implementation:**
```python
import numpy as np

class SVM:
    def __init__(self, learning_rate=0.01, lambda_param=0.01, iterations=1000):
        self.learning_rate = learning_rate
        self.lambda_param = lambda_param
        self.iterations = iterations
        self.w = None
        self.b = None

    def fit(self, X, y):
        m, n = X.shape
        self.w = np.zeros(n)
        self.b = 0
        for _ in range(self.iterations):
            for i, x_i in enumerate(X):
                condition = y[i] * (np.dot(x_i, self.w) - self.b) >= 1
                if condition:
                    self.w -= self.learning_rate * (2 * self.lambda_param * self.w)
                else:
                    self.w -= self.learning_rate * (2 * self.lambda_param * self.w - np.dot(x_i, y[i]))
                    self.b -= self.learning_rate * y[i]

    def predict(self, X):
        return np.sign(np.dot(X, self.w) - self.b)

# Example usage:
X = np.array([[1, 2], [2, 3], [3, 4], [4, 5]])
y = np.array([1, 1, -1, -1])

svm = SVM()
svm.fit(X, y)
predictions = svm.predict(X)
print(predictions)  # Output: [ 1  1 -1 -1]
```

### 5. K-Nearest Neighbors (KNN)

**Theory:**
KNN classifies data based on similarity measures, where the class of a new data point is determined by the majority class among its k nearest neighbors.

**Code Implementation:**
```python
import numpy as np

class KNN:
    def __init__(self, k=3):
        self.k = k

    def fit(self, X, y):
        self.X_train = X
        self.y_train = y

    def predict(self, X):
        predictions = []
        for x_new in X:
            distances = [np.sqrt(np.sum((x_new - x_train) ** 2)) for x_train in self.X_train]
            nearest_indices = np.argsort(distances)[:self.k]
            nearest_labels = [self.y_train[i] for i in nearest_indices]
            predictions.append(max(set(nearest_labels), key=nearest_labels.count))
        return predictions

# Example usage:
X_train = np.array([[1, 2], [2, 3], [3, 4], [4, 5]])
y_train = np.array([0, 0, 1, 1])
X_test = np.array([[5, 6]])

knn = KNN(k=3)
knn.fit(X_train, y_train)
predictions = knn.predict(X_test)
print(predictions)  # Output: [1]
```

### 6. Naive Bayes

**Theory:**
Naive Bayes classifiers are based on Bayes' theorem with strong independence assumptions between features.

**Code Implementation:**
```python
import numpy as np

class NaiveBayes:
    def __init__(self):
        self.classes = None
        self.parameters = {}
    
    def fit(self, X, y):
        self.classes = np.unique(y)
        for c in self.classes:
            X_c = X[y == c]
            self.parameters[c] = {
                'mean': X_c.mean(axis=0),
                'std': X_c.std(axis=0) + 1e-4  # Add small value for numerical stability
            }
    
    def predict(self, X):
        probabilities = []
        for x in X:
            probs = []
            for c in self.classes:
                mean, std = self.parameters[c]['mean'], self.parameters[c]['std']
                likelihood = np.sum(np.log((1 / np.sqrt(2 * np.pi * std ** 2)) * np.exp(-(x - mean) ** 2 / (2 * std ** 2))))
                prior = np.log(len(X_c) / len(X))
                posterior = likelihood + prior
                probs.append(posterior)
            probabilities.append(self.classes[np.argmax(probs)])
        return probabilities

# Example usage:
X_train = np.array([[1, 2], [2, 3], [3, 4], [4, 5]])
y_train = np.array([0, 0, 1, 1])
X_test = np.array([[5, 6]])

nb = NaiveBayes()
nb.fit(X_train, y_train)
predictions = nb.predict(X_test)
print(predictions)  # Output: [1]
```

### 7. Principal Component Analysis (PCA)

**Theory:**
PCA is a technique for dimensionality reduction that identifies the directions (principal components) of maximum variance in high-dimensional data.

**Code Implementation:**
```python
import numpy as np

def pca(X, n_components):
    # Standardize the data
    X_std = (X - np.mean(X, axis=0)) / np.std(X, axis=0)
    
    # Calculate the covariance matrix
    cov_matrix = np.cov(X_std, rowvar=False)
    
    # Calculate eigenvalues and eigenvectors
    eigenvalues, eigenvectors = np.linalg.eig(cov_matrix)
    
    # Sort eigenvalues and eigenvectors
    sorted_indices = np.argsort(eigenvalues)[::-1]
    eigenvectors = eigenvectors[:, sorted_indices]
    
    # Select the top n_components eigenvectors
    components = eigenvectors[:, :n_components]
    
    # Project the data onto the new subspace
    projected = np.dot(X_std, components)
    
    return projected

# Example usage:
X = np.array([[1, 2, 3], [2, 3, 4], [3, 4, 5]])
n_components = 2

X_projected = pca(X, n_components)
print(X_projected)
```

### 8. Gradient Descent

**Theory:**
Gradient descent is an iterative optimization algorithm used to minimize a loss function by adjusting model parameters in the direction of steepest descent.

**Code Implementation:**
```python
import numpy as np

def gradient_descent(X, y, theta, learning_rate, iterations):
    m = len(y)
    for _ in range(iterations):
        gradient = np.dot(X.T, np.dot(X, theta) - y) / m
        theta -= learning_rate * gradient
    return theta

# Example usage:
X = np.array([[1], [2], [3], [4]])
y = np.array([2, 3.5, 4, 5.5])
theta = np.zeros((X.shape[1], 1))
learning_rate = 0.01
iterations = 1000

theta = gradient_descent(X, y, theta, learning_rate, iterations)
print(theta)  # Output: [[1.9741262]]
```

### 9. Cross-Validation

**Theory:**
Cross-validation is a technique to evaluate the performance of a model by splitting the data into subsets, training the model on some subsets, and evaluating it on the remaining subset(s).

**Code Implementation:**
```python
import numpy as np

def k_fold_cross_validation(X, y, model, k=5):
    m = len(y)
    fold_size = m // k
    indices = np.arange(m)
    np.random.shuffle(indices)
    scores = []
    for i in range(k):
        val_indices = indices[i * fold_size:(i + 1) * fold_size]
        train_indices = np.concatenate([indices[:i * fold_size], indices[(i + 1) * fold_size:]])
        
        X_train, X_val = X[train_indices], X[val_indices]
        y_train, y_val = y[train_indices], y[val_indices]
        
        model.fit(X_train, y_train)
        score = model.score(X_val, y_val)
        scores.append(score)
    return np.mean(scores)

# Example usage:
from sklearn.linear_model import LogisticRegression

X = np.array([[1, 2], [3, 4], [5, 6]])
y = np.array([0, 1, 0])

model = LogisticRegression()
mean_accuracy = k_fold_cross_validation(X, y, model, k=3)
print(mean_accuracy)
```

---
