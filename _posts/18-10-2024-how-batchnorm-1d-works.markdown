---
layout: post
title:  "How Batchnorm 1d works"
date:   2024-10-18 00:04:58 +0530
categories: machine-learning
summary: Math behind batchnorm 1d
---

# **Batch Normalization 1D Explained with a Simple Example**

Batch normalization (BatchNorm) is an essential concept in deep learning, helping models converge faster and perform better by stabilizing the learning process. In this article, I’ll walk you through **BatchNorm1d**—a version used for **1D data**, such as sequential inputs or dense layers.

This article includes:
- What BatchNorm1d does
- Step-by-step calculations
- A practical example with code-friendly explanations

---

## **What is Batch Normalization 1D?**

Batch normalization is a technique to normalize the input layer by **scaling and shifting** the inputs to have a **mean of 0** and **variance of 1** across the batch. This ensures that the input to the next layer stays within a stable range, which improves training speed and generalization.

For **1D data** with shape `(batch_size, num_features)`, BatchNorm1d operates across the **features dimension** for each batch.

---

### **The Formula for Batch Normalization**

Let’s break it down:
\[
\hat{x_i} = \frac{x_i - \mu}{\sqrt{\sigma^2 + \epsilon}}
\]

\[
y_i = \gamma \hat{x_i} + \beta
\]

Where:
- \(x_i\) = Input value
- \(\mu\) = Mean of the feature across the batch  
- \(\sigma^2\) = Variance of the feature across the batch  
- \(\epsilon\) = A small constant to prevent division by zero  
- \(\gamma\) = Learnable scale parameter  
- \(\beta\) = Learnable shift parameter  

This process standardizes the input data and applies **optional scaling and shifting** via the learnable parameters \( \gamma \) and \( \beta \).

---

## **Step-by-Step Example of BatchNorm1d**  

Let’s assume the following input batch:

\[
X = 
\begin{bmatrix}
1.0 & 2.0 \\
2.0 & 4.0 \\
3.0 & 6.0
\end{bmatrix}
\]

- **Batch size**: 3  
- **Number of features**: 2  

We will apply BatchNorm1d on this batch step by step.

---

### **Step 1: Calculate the Mean (\(\mu\))**  

We calculate the **mean** of each feature across the batch.  

\[
\mu_1 = \frac{1.0 + 2.0 + 3.0}{3} = 2.0
\]
\[
\mu_2 = \frac{2.0 + 4.0 + 6.0}{3} = 4.0
\]

So,  
\(\mu = [2.0, 4.0]\)

---

### **Step 2: Calculate the Variance (\(\sigma^2\))**  

Next, we calculate the **variance** of each feature across the batch.

\[
\sigma_1^2 = \frac{(1.0 - 2.0)^2 + (2.0 - 2.0)^2 + (3.0 - 2.0)^2}{3} = \frac{1.0 + 0.0 + 1.0}{3} = 0.67
\]

\[
\sigma_2^2 = \frac{(2.0 - 4.0)^2 + (4.0 - 4.0)^2 + (6.0 - 4.0)^2}{3} = \frac{4.0 + 0.0 + 4.0}{3} = 2.67
\]

So,  
\(\sigma^2 = [0.67, 2.67]\)

---

### **Step 3: Normalize the Input Values (\(\hat{x_i}\))**  

We use the formula:

\[
\hat{x_i} = \frac{x_i - \mu}{\sqrt{\sigma^2 + \epsilon}}
\]

Assuming \(\epsilon = 10^{-5}\), the normalized values are:

For **Feature 1**:
\[
\hat{x_{1,1}} = \frac{1.0 - 2.0}{\sqrt{0.67 + 10^{-5}}} = \frac{-1.0}{0.82} \approx -1.22
\]
\[
\hat{x_{2,1}} = \frac{2.0 - 2.0}{\sqrt{0.67 + 10^{-5}}} = 0.0
\]
\[
\hat{x_{3,1}} = \frac{3.0 - 2.0}{\sqrt{0.67 + 10^{-5}}} = \frac{1.0}{0.82} \approx 1.22
\]

For **Feature 2**:
\[
\hat{x_{1,2}} = \frac{2.0 - 4.0}{\sqrt{2.67 + 10^{-5}}} = \frac{-2.0}{1.63} \approx -1.23
\]
\[
\hat{x_{2,2}} = \frac{4.0 - 4.0}{\sqrt{2.67 + 10^{-5}}} = 0.0
\]
\[
\hat{x_{3,2}} = \frac{6.0 - 4.0}{\sqrt{2.67 + 10^{-5}}} = \frac{2.0}{1.63} \approx 1.23
\]

The normalized values are:

\[
\hat{X} = 
\begin{bmatrix}
-1.22 & -1.23 \\
0.0 & 0.0 \\
1.22 & 1.23
\end{bmatrix}
\]

---

### **Step 4: Apply Learnable Parameters (\(\gamma\) and \(\beta\))**  

Let’s assume:
\[
\gamma = [1.0, 1.0], \quad \beta = [0.0, 0.0]
\]

Since both \(\gamma\) and \(\beta\) are identity values in this case, the final output will remain:

\[
Y = \hat{X} = 
\begin{bmatrix}
-1.22 & -1.23 \\
0.0 & 0.0 \\
1.22 & 1.23
\end{bmatrix}
\]

---

## **Summary**

This is how **BatchNorm1d** works. It normalizes each feature across the batch to have a mean of **0** and a variance of **1**. Optionally, it scales and shifts the results using learnable parameters \( \gamma \) and \( \beta \).

---

### **Key Takeaways**

- BatchNorm helps stabilize and accelerate training.
- For **1D inputs**, it normalizes across the batch along the features dimension.
- Learnable parameters \( \gamma \) and \( \beta \) allow the model to scale and shift the normalized outputs for better performance.

---

Feel free to ask questions or share your thoughts in the comments!

---

### **Next Steps**

If you found this article helpful, try experimenting with **PyTorch** or **TensorFlow** to implement BatchNorm1d yourself. You’ll get an even deeper understanding by applying it in practice.

Happy learning! 🚀
