# Backpropagation Details – Optimizing Multiple Parameters Simultaneously  

## **1. Introduction to Multi-Parameter Optimization**  
Backpropagation extends to optimizing **multiple parameters** (weights and biases) in neural networks simultaneously. This lesson demonstrates how to update three parameters (\( w_3, w_4, b_3 \)) using the **chain rule** and **gradient descent**, building on the foundational ideas from single-parameter optimization.  

---

## **2. Core Components**  

### **2.1 Neural Network Setup**  
- **Input**: Drug dosage (\( \text{Input}_i \), where \( i = 1, 2, 3 \)).  
- **Hidden Layers**:  
  - **Top Node**: Computes \( x_{1,i} = \text{Input}_i \cdot w_1 + b_1 \), then applies SoftPlus activation to get \( y_{1,i} \).  
  - **Bottom Node**: Computes \( x_{2,i} = \text{Input}_i \cdot w_2 + b_2 \), then applies SoftPlus activation to get \( y_{2,i} \).  
- **Output**:  
  - Predicted = \( (y_{1,i} \cdot w_3) + (y_{2,i} \cdot w_4) + b_3 \).  

### **2.2 Loss Function**  
- **Sum of Squared Residuals (SSR)**:  
  \( \text{SSR} = \sum_{i=1}^3 (\text{Observed}_i - \text{Predicted}_i)^2 \).  
- **Goal**: Minimize SSR by optimizing \( w_3, w_4, b_3 \).  

---

## **3. Step-by-Step Backpropagation**  

### **3.1 Initialize Parameters**  
1. **Weights**: \( w_3, w_4 \) initialized randomly (e.g., from a normal distribution).  
2. **Bias**: \( b_3 = 0 \).  
3. **Result**: Initial green squiggle (predictions) with SSR = 1.4.  

### **3.2 Compute Derivatives Using the Chain Rule**  
For each parameter, calculate:  
\[ \frac{\partial \text{SSR}}{\partial \text{Parameter}} = \frac{\partial \text{SSR}}{\partial \text{Predicted}} \times \frac{\partial \text{Predicted}}{\partial \text{Parameter}} \]  

#### **For \( w_3 \):**  
1. **Term 1**: \( \frac{\partial \text{SSR}}{\partial \text{Predicted}} = -2 \sum (\text{Observed}_i - \text{Predicted}_i) \).  
2. **Term 2**: \( \frac{\partial \text{Predicted}}{\partial w_3} = y_{1,i} \).  
3. **Final Derivative**:  
   \( \frac{\partial \text{SSR}}{\partial w_3} = -2 \sum (\text{Observed}_i - \text{Predicted}_i) \cdot y_{1,i} \).  

#### **For \( w_4 \):**  
1. **Term 1**: Same as above.  
2. **Term 2**: \( \frac{\partial \text{Predicted}}{\partial w_4} = y_{2,i} \).  
3. **Final Derivative**:  
   \( \frac{\partial \text{SSR}}{\partial w_4} = -2 \sum (\text{Observed}_i - \text{Predicted}_i) \cdot y_{2,i} \).  

#### **For \( b_3 \):**  
1. **Term 1**: Same as above.  
2. **Term 2**: \( \frac{\partial \text{Predicted}}{\partial b_3} = 1 \).  
3. **Final Derivative**:  
   \( \frac{\partial \text{SSR}}{\partial b_3} = -2 \sum (\text{Observed}_i - \text{Predicted}_i) \).  

### **3.3 Gradient Descent Updates**  
1. **Learning Rate**: Set to 0.01 (adjusts step size).  
2. **Update Equations**:  
   - \( w_3^{\text{new}} = w_3^{\text{old}} - (\text{Learning Rate} \times \frac{\partial \text{SSR}}{\partial w_3}) \).  
   - \( w_4^{\text{new}} = w_4^{\text{old}} - (\text{Learning Rate} \times \frac{\partial \text{SSR}}{\partial w_4}) \).  
   - \( b_3^{\text{new}} = b_3^{\text{old}} - (\text{Learning Rate} \times \frac{\partial \text{SSR}}{\partial b_3}) \).  

**Example**:  
- Initial \( w_3 = 0.36, w_4 = 0.63, b_3 = 0 \).  
- After first iteration:  
  - \( \frac{\partial \text{SSR}}{\partial w_3} = 2.58 \) → New \( w_3 \).  
  - \( \frac{\partial \text{SSR}}{\partial w_4} \) and \( \frac{\partial \text{SSR}}{\partial b_3} \) similarly updated.  

### **3.4 Iterate Until Convergence**  
- Repeat derivative calculations and updates until:  
  - Step sizes become very small (e.g., < 0.001).  
  - Maximum iterations reached (e.g., 1000 steps).  

---

## **4. Key Concepts**  

### **4.1 Chain Rule in Multi-Parameter Optimization**  
- **Shared Term**: \( \frac{\partial \text{SSR}}{\partial \text{Predicted}} \) is reused for all parameters, simplifying calculations.  
- **Modular Updates**: Each parameter’s derivative depends only on its direct contribution to predictions.  

### **4.2 Simultaneous Optimization**  
- **Parallel Updates**: Adjust \( w_3, w_4, b_3 \) together in each iteration.  
- **Interdependence**: Changing one parameter affects the green squiggle, requiring coordinated updates.  

### **4.3 Learning Rate Sensitivity**  
- **Balancing Act**: Small learning rates ensure stability but slow convergence; adaptive methods (e.g., Adam) mitigate this.  

---

## **5. Practical Takeaways**  
1. **Efficiency**: Backpropagation computes gradients for all parameters in one forward-backward pass.  
2. **Scalability**: The same framework applies to neural networks with thousands of parameters.  
3. **Debugging**: Monitor SSR and gradients to detect issues like vanishing/exploding gradients.  

---

## **6. Summary**  
Backpropagation optimizes multiple parameters by:  
1. Calculating gradients via the **chain rule**.  
2. Updating parameters using **gradient descent**.  
3. Iterating until convergence.  
This method scales to complex models, making neural networks adaptable to diverse datasets.  
