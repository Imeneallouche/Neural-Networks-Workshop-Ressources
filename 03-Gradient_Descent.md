# Lesson: Gradient Descent – Step-by-Step Optimization  

## **1. Introduction to Gradient Descent**  
Gradient Descent is an iterative optimization algorithm used to **minimize a loss function** (e.g., sum of squared residuals) by adjusting model parameters. It is widely used in machine learning and statistics when analytical solutions (e.g., least squares) are impractical.  

---

## **2. Core Components**  

### **2.1 Loss Function**  
- **Purpose**: Quantifies model error (e.g., **Sum of Squared Residuals** for linear regression).  
- **Example**: For a line

  ![image](https://github.com/user-attachments/assets/06d851cd-2e45-4126-9210-bfba06a4c65e)

  ![image](https://github.com/user-attachments/assets/d827007e-6dd7-4c64-9065-68bd3d3cd5b8)

### **2.2 Learning Rate**  
- **Role**: Controls step size during parameter updates.  
  - **Too High**: May overshoot the minimum.  
  - **Too Low**: Slows convergence.  
- **Default Practice**: Start with a small value (e.g., 0.01) or use adaptive methods.  

### **2.3 Gradient**  
- **Definition**: Vector of partial derivatives of the loss function with respect to each parameter.  
- **Example**: For parameters \( \text{Intercept} \) and \( \text{Slope} \), compute:

  ![image](https://github.com/user-attachments/assets/98a148b7-7dcc-46fc-af20-f20a67563be4)


---

## **3. Step-by-Step Process**  

### **3.1 Single Parameter Optimization (Intercept)**  
1. **Initialize**: Set a random intercept (e.g., 0).  
2. **Calculate Residuals**: Predict heights using current intercept.  
3. **Compute Gradient**:  

    ![image](https://github.com/user-attachments/assets/c063e8a0-9d3a-4321-ad64-0eb50b60e3b6)

4. **Update Intercept**:  

   ![image](https://github.com/user-attachments/assets/bd2b575c-052c-4388-bf9a-d942c9ec978b)

5. **Repeat**: Until gradient ≈ 0 (indicating convergence).  

**Example**:  
- Initial intercept = 0 → SSR = 3.1.  
- First step: Gradient = -5.7 → New intercept = 0.57 (learning rate = 0.1).  
- Converges to intercept = 0.95 (matches least squares).  

### **3.2 Multiple Parameter Optimization (Intercept + Slope)**  
1. **Initialize**: Random values for intercept and slope (e.g., 0 and 1).  
2. **Compute Gradients**:  

    ![image](https://github.com/user-attachments/assets/670efbcc-2f50-4229-aa54-ccc08820ffa9)

3. **Update Parameters**:  

   ![image](https://github.com/user-attachments/assets/14d83636-21c1-45ce-ace9-06b04f74040c)

4. **Repeat**: Until all gradients are near zero.  

**Example**:  
- Initial: Intercept = 0, Slope = 1 → SSR = high.  
- After steps: Converges to Intercept = 0.95, Slope = 0.64 (same as least squares).  

---

## **4. Advanced Topics**  

### **4.1 Stochastic Gradient Descent (SGD)**  
- **Purpose**: Accelerate training on large datasets.  
- **Method**: Use **random subsets (mini-batches)** of data to compute gradients at each step.  
- **Advantages**: Faster computation, avoids local minima.  

### **4.2 Learning Rate Strategies**  
- **Adaptive Learning Rates**: Automatically adjust based on gradient magnitudes (e.g., Adam optimizer).  
- **Learning Rate Decay**: Reduce learning rate over time for finer adjustments.  

---

## **5. Practical Takeaways**  
- **Why Gradient Descent?** Essential for complex models (e.g., neural networks) where analytical solutions don’t exist.  
- **Parameter Sensitivity**: Learning rate and initial guesses impact convergence speed and accuracy.  
- **Universal Application**: Same steps apply to any loss function (e.g., logistic regression, neural networks).  

---

## **6. Summary**  
Gradient Descent minimizes loss functions by iteratively adjusting parameters based on gradients. Key steps include:  
1. Compute gradients (derivatives).  
2. Update parameters using learning rate.  
3. Repeat until convergence.  
Variants like **Stochastic Gradient Descent** enhance scalability for large datasets.  
