# Backpropagation Details – Applying the Chain Rule to All Parameters  

## **1. Introduction to Full-Parameter Optimization**  
This lesson dives into optimizing **all parameters** (weights and biases) in a neural network simultaneously using the **chain rule** and **gradient descent**. By extending previous concepts, we demonstrate how to train a neural network to fit complex data patterns (the "green squiggle") by adjusting every parameter iteratively.  

---

## **2. Core Components**  

### **2.1 Neural Network Architecture**  
- **Input Layer**: Drug dosage (\( \text{Input}_i \), \( i = 1, 2, 3 \)).  
- **Hidden Layers**:  
  - **Top Node**: \( x_{1,i} = \text{Input}_i \cdot w_1 + b_1 \) → SoftPlus activation → \( y_{1,i} \).  
  - **Bottom Node**: \( x_{2,i} = \text{Input}_i \cdot w_2 + b_2 \) → SoftPlus activation → \( y_{2,i} \).  
- **Output Layer**:  
  - Predicted = \( (y_{1,i} \cdot w_3) + (y_{2,i} \cdot w_4) + b_3 \).  

### **2.2 Loss Function**  
- **Sum of Squared Residuals (SSR)**:  
  \( \text{SSR} = \sum_{i=1}^3 (\text{Observed}_i - \text{Predicted}_i)^2 \).  
- **Goal**: Minimize SSR by optimizing \( w_1, b_1, w_2, b_2, w_3, w_4, b_3 \).  

---

## **3. Step-by-Step Backpropagation**  

### **3.1 Initialize All Parameters**  
1. **Weights**: \( w_1, w_2, w_3, w_4 \) initialized randomly (e.g., from a normal distribution).  
2. **Biases**: \( b_1, b_2, b_3 = 0 \).  
3. **Result**: Initial green squiggle poorly fits data (e.g., SSR = high).  

### **3.2 Compute Derivatives for All Parameters**  
For each parameter, apply the chain rule:  
\[ \frac{\partial \text{SSR}}{\partial \text{Parameter}} = \frac{\partial \text{SSR}}{\partial \text{Predicted}} \times \frac{\partial \text{Predicted}}{\partial \text{Parameter}} \]  

#### **Example: Derivative for \( w_1 \)**  
1. **Term 1**: \( \frac{\partial \text{SSR}}{\partial \text{Predicted}} = -2 \sum (\text{Observed}_i - \text{Predicted}_i) \).  
2. **Term 2**: \( \frac{\partial \text{Predicted}}{\partial y_{1,i}} = w_3 \).  
3. **Term 3**: \( \frac{\partial y_{1,i}}{\partial x_{1,i}} = \frac{e^{x_{1,i}}}{1 + e^{x_{1,i}}} \) (derivative of SoftPlus).  
4. **Term 4**: \( \frac{\partial x_{1,i}}{\partial w_1} = \text{Input}_i \).  
5. **Final Derivative**:  
   \( \frac{\partial \text{SSR}}{\partial w_1} = -2 \sum (\text{Observed}_i - \text{Predicted}_i) \cdot w_3 \cdot \frac{e^{x_{1,i}}}{1 + e^{x_{1,i}}} \cdot \text{Input}_i \).  

#### **Example: Derivative for \( b_1 \)**  
1. **Term 1–3**: Same as \( w_1 \).  
2. **Term 4**: \( \frac{\partial x_{1,i}}{\partial b_1} = 1 \).  
3. **Final Derivative**:  
   \( \frac{\partial \text{SSR}}{\partial b_1} = -2 \sum (\text{Observed}_i - \text{Predicted}_i) \cdot w_3 \cdot \frac{e^{x_{1,i}}}{1 + e^{x_{1,i}}} \cdot 1 \).  

#### **Repeat for \( w_2, b_2 \)**  
- Replace \( w_1 \rightarrow w_2 \), \( b_1 \rightarrow b_2 \), \( x_{1,i} \rightarrow x_{2,i} \), \( y_{1,i} \rightarrow y_{2,i} \), \( w_3 \rightarrow w_4 \).  

### **3.3 Gradient Descent Updates**  
1. **Learning Rate**: Set to a small value (e.g., 0.01).  
2. **Update All Parameters**:  
   - \( \text{Parameter}^{\text{new}} = \text{Parameter}^{\text{old}} - (\text{Learning Rate} \times \frac{\partial \text{SSR}}{\partial \text{Parameter}}) \).  

**Example**:  
- Initial \( w_1 = 1.5 \), \( b_1 = 0 \), \( w_2 = -0.8 \), \( b_2 = 0 \).  
- After first iteration:  
  - \( \frac{\partial \text{SSR}}{\partial w_1} = 0.76 \) → Update \( w_1 \).  
  - Similarly update \( b_1, w_2, b_2 \).  

### **3.4 Iterate Until Convergence**  
- **Stopping Criteria**:  
  - Step sizes < threshold (e.g., 0.001).  
  - Maximum steps (e.g., 1000 iterations).  
- **Result**: Green squiggle fits data after ~450 steps.  

---

## **4. Key Concepts**  

### **4.1 Chain Rule in Depth**  
- **Modularity**: Derivatives reuse intermediate terms (e.g., \( \frac{\partial \text{SSR}}{\partial \text{Predicted}} \)), reducing redundant calculations.  
- **Activation Derivatives**: SoftPlus derivative \( \frac{e^{x}}{1 + e^{x}} \) ensures smooth gradient flow.  

### **4.2 Simultaneous Parameter Updates**  
- **Interconnected Parameters**: Adjusting \( w_1 \) affects \( y_{1,i} \), which impacts \( w_3 \), and so on.  
- **Coordinated Learning**: All parameters adjust in tandem to minimize SSR efficiently.  

### **4.3 Initialization Strategies**  
- **Weights**: Random initialization (e.g., normal distribution) breaks symmetry.  
- **Biases**: Typically initialized to 0.  

---

## **5. Practical Takeaways**  
1. **Scalability**: This method scales to networks with millions of parameters.  
2. **Debugging Tools**: Monitor gradients to detect vanishing/exploding gradients.  
3. **Adaptive Learning**: Use techniques like Adam optimizer for dynamic learning rates.  

---

## **6. Summary**  
Backpropagation trains neural networks by:  
1. Calculating gradients for **all parameters** via the chain rule.  
2. Updating parameters simultaneously using **gradient descent**.  
3. Iterating until the model fits the data (green squiggle).  
This approach underpins modern deep learning, enabling models to learn from complex datasets.  
