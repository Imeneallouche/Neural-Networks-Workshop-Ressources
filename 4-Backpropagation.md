# Backpropagation in Neural Networks – Optimizing Parameters  

## **1. Introduction to Backpropagation**  
Backpropagation is an algorithm used to **train neural networks** by optimizing weights and biases. It combines the **chain rule** (for calculating derivatives) with **gradient descent** (for minimizing loss functions). This lesson breaks down how backpropagation adjusts the final bias term (\( b_3 \)) in a neural network to fit data.  

---

## **2. Core Components**  

### **2.1 Neural Network Setup**  
- **Input**: Drug dosage (0 = low, 1 = high).  
- **Output**: Predicted effectiveness (0 or 1).  
- **Architecture**:  
  - **Hidden Layer**: Two nodes with SoftPlus activation.  
  - **Parameters**: Weights (\( w_1, w_2, w_3, w_4 \)) and biases (\( b_1, b_2, b_3 \)).  
  - **Final Output**: Green squiggle = (Blue curve + Orange curve) + \( b_3 \).  

### **2.2 Loss Function**  
- **Sum of Squared Residuals (SSR)**: Measures prediction error.  
  - Example: SSR = \( (0 - \text{Predicted})^2 + (1 - \text{Predicted})^2 + (0 - \text{Predicted})^2 \).  
- **Goal**: Minimize SSR by optimizing \( b_3 \).  

---

## **3. Step-by-Step Backpropagation**  

### **3.1 Initial Setup**  
1. **Initialize Parameters**: Set \( b_3 = 0 \).  
2. **Calculate Initial SSR**:  
   - Predicted values from the green squiggle (e.g., SSR = 20.4 when \( b_3 = 0 \)).  

### **3.2 Chain Rule Application**  
- **Derivative of SSR w.r.t \( b_3 \)** = \( \frac{\partial \text{SSR}}{\partial \text{Predicted}} \times \frac{\partial \text{Predicted}}{\partial b_3} \).  
  1. **First Term**:  
     - \( \frac{\partial \text{SSR}}{\partial \text{Predicted}} = -2 \sum (\text{Observed} - \text{Predicted}) \).  
  2. **Second Term**:  
     - \( \frac{\partial \text{Predicted}}{\partial b_3} = 1 \) (since Predicted = Blue + Orange + \( b_3 \)).  
  3. **Final Derivative**:  
     - \( \frac{\partial \text{SSR}}{\partial b_3} = -2 \sum (\text{Observed} - \text{Predicted}) \).  

### **3.3 Gradient Descent**  
1. **Compute Gradient**:  
   - At \( b_3 = 0 \), gradient = -15.7.  
2. **Update \( b_3 \)** with learning rate (e.g., 0.1):  
   - Step Size = \( -15.7 \times 0.1 = -1.57 \).  
   - New \( b_3 = 0 - (-1.57) = 1.57 \).  
3. **Repeat**:  
   - Recalculate SSR and gradient until step size ≈ 0 (e.g., \( b_3 = 2.61 \), SSR = 0.46).  

---

## **4. Visualizing Parameter Optimization**  
- **SSR vs \( b_3 \) Curve**:  
  - Initial \( b_3 = 0 \) → SSR = 20.4.  
  - After updates: \( b_3 = 2.61 \) → SSR ≈ 0.46 (minimum).  
- **Effect of \( b_3 \)**: Adjusting \( b_3 \) shifts the green squiggle vertically to align predictions with observed data.  

---

## **5. Key Concepts**  

### **5.1 Chain Rule in Backpropagation**  
- **Forward Pass**: Compute predictions using current parameters.  
- **Backward Pass**: Calculate derivatives backward from the loss to parameters.  

### **5.2 Role of Gradient Descent**  
- **Learning Rate**: Controls step size (e.g., 0.1 ensures stable convergence).  
- **Termination**: Stop when step size < threshold (e.g., 0.001) or after maximum iterations.  

### **5.3 Generalization to All Parameters**  
- **Multiple Parameters**: Apply the same steps to optimize \( w_1, w_2, b_1 \), etc.  
- **Simultaneous Optimization**: Update all parameters iteratively using their respective gradients.  

---

## **6. Practical Takeaways**  
- **Why Backpropagation?** Efficiently trains complex neural networks by leveraging calculus and optimization.  
- **Loss Function Sensitivity**: SSR penalizes large errors, guiding parameters toward better fits.  
- **Universal Workflow**:  
  1. Forward pass → Compute loss.  
  2. Backward pass → Calculate gradients.  
  3. Update parameters → Repeat until convergence.  

---

## **7. Summary**  
Backpropagation minimizes prediction errors by:  
1. Calculating gradients using the **chain rule**.  
2. Updating parameters with **gradient descent**.  
This process, applied iteratively, enables neural networks to learn from data.  
