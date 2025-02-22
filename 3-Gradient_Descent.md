# Lesson: Gradient Descent – Step-by-Step Optimization  

## **1. Introduction to Gradient Descent**  
Gradient Descent is an iterative optimization algorithm used to **minimize a loss function** (e.g., sum of squared residuals) by adjusting model parameters. It is widely used in machine learning and statistics when analytical solutions (e.g., least squares) are impractical.  

---

## **2. Core Components**  

### **2.1 Loss Function**  
- **Purpose**: Quantifies model error (e.g., **Sum of Squared Residuals** for linear regression).  
- **Example**: For a line \( \text{Height} = \text{Intercept} + \text{Slope} \times \text{Weight} \),  
  \( \text{SSR} = \sum (\text{Observed Height} - \text{Predicted Height})^2 \).  

### **2.2 Learning Rate**  
- **Role**: Controls step size during parameter updates.  
  - **Too High**: May overshoot the minimum.  
  - **Too Low**: Slows convergence.  
- **Default Practice**: Start with a small value (e.g., 0.01) or use adaptive methods.  

### **2.3 Gradient**  
- **Definition**: Vector of partial derivatives of the loss function with respect to each parameter.  
- **Example**: For parameters \( \text{Intercept} \) and \( \text{Slope} \), compute:  
  - \( \frac{\partial \text{SSR}}{\partial \text{Intercept}} \),  
  - \( \frac{\partial \text{SSR}}{\partial \text{Slope}} \).  

---

## **3. Step-by-Step Process**  

### **3.1 Single Parameter Optimization (Intercept)**  
1. **Initialize**: Set a random intercept (e.g., 0).  
2. **Calculate Residuals**: Predict heights using current intercept.  
3. **Compute Gradient**:  
   - \( \frac{\partial \text{SSR}}{\partial \text{Intercept}} = -2 \sum (\text{Observed} - \text{Predicted}) \).  
4. **Update Intercept**:  
   - \( \text{New Intercept} = \text{Old Intercept} - (\text{Learning Rate} \times \text{Gradient}) \).  
5. **Repeat**: Until gradient ≈ 0 (indicating convergence).  

**Example**:  
- Initial intercept = 0 → SSR = 3.1.  
- First step: Gradient = -5.7 → New intercept = 0.57 (learning rate = 0.1).  
- Converges to intercept = 0.95 (matches least squares).  

### **3.2 Multiple Parameter Optimization (Intercept + Slope)**  
1. **Initialize**: Random values for intercept and slope (e.g., 0 and 1).  
2. **Compute Gradients**:  
   - \( \frac{\partial \text{SSR}}{\partial \text{Intercept}} = -2 \sum (\text{Observed} - \text{Predicted}) \),  
   - \( \frac{\partial \text{SSR}}{\partial \text{Slope}} = -2 \sum \text{Weight} \times (\text{Observed} - \text{Predicted}) \).  
3. **Update Parameters**:  
   - \( \text{New Param} = \text{Old Param} - (\text{Learning Rate} \times \text{Gradient}) \).  
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
