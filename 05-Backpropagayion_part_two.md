# Backpropagation Details – Optimizing Multiple Parameters Simultaneously  

## **1. Introduction to Multi-Parameter Optimization**  
Backpropagation extends to optimizing **multiple parameters** (weights and biases) in neural networks simultaneously. This lesson demonstrates how to update three parameters (\( w_3, w_4, b_3 \)) using the **chain rule** and **gradient descent**, building on the foundational ideas from single-parameter optimization.  

---

## **2. Core Components**  

### **2.1 Neural Network Setup**  
- **Input**: Drug dosage (Input_i, where i = 1, 2, 3).  
- **Hidden Layers**:  
  - **Top Node**: Computes

    ![image](https://github.com/user-attachments/assets/cdea0d60-370d-4c55-8e54-4c598d533337)
  
then applies SoftPlus activation to get y{1,i}.  
  - **Bottom Node**: Computes

    ![image](https://github.com/user-attachments/assets/c7b3c1a2-599c-4723-b83d-f58dab727e6b)

, then applies SoftPlus activation to get y{2,i}  

- **Output**:

  ![image](https://github.com/user-attachments/assets/081c0cbe-8d3a-4396-a49f-a6681769267b)

### **2.2 Loss Function**  
- **Sum of Squared Residuals (SSR)**:

  ![image](https://github.com/user-attachments/assets/430c4ab2-5688-4101-a87b-28c0824d8047)

- **Goal**: Minimize SSR by optimizing w3, w4, b3.  

---

## **3. Step-by-Step Backpropagation**  

### **3.1 Initialize Parameters**  
1. **Weights**: w3, w4  initialized randomly (e.g., from a normal distribution).  
2. **Bias**: b3 = 0.  
3. **Result**: Initial green squiggle (predictions) with SSR = 1.4.  

### **3.2 Compute Derivatives Using the Chain Rule**  
For each parameter, calculate:  

![image](https://github.com/user-attachments/assets/6d68f3f5-cffc-40a7-a8af-bc69cf103750)

#### **For w3:**  

![image](https://github.com/user-attachments/assets/945d589d-1dc2-4c15-9439-701cbf8cc854)


#### **For w4:**  

 ![image](https://github.com/user-attachments/assets/cf4ce13f-48b8-44a4-befe-33f577a2fb34)


#### **For b3:**  

 ![image](https://github.com/user-attachments/assets/9c33f52a-b359-4ab6-8055-e9f834451292)


### **3.3 Gradient Descent Updates**  
1. **Learning Rate**: Set to 0.01 (adjusts step size).  
2. **Update Equations**:  

   ![image](https://github.com/user-attachments/assets/18b1f21f-7899-4318-98c3-5088ad86d676)


**Example**:  
- Initial w3 = 0.36, w4 = 0.63, b3 = 0.  
- After first iteration:
  
  ![image](https://github.com/user-attachments/assets/c6b6e94e-83c0-4e2d-8015-1c8f44109acb)
 

### **3.4 Iterate Until Convergence**  
- Repeat derivative calculations and updates until:  
  - Step sizes become very small (e.g., < 0.001).  
  - Maximum iterations reached (e.g., 1000 steps).  

---

## **4. Key Concepts**  

### **4.1 Chain Rule in Multi-Parameter Optimization**  
- **Shared Term**:

  ![image](https://github.com/user-attachments/assets/1c28e27b-166c-406c-9448-7fb966d77e53)

 is reused for all parameters, simplifying calculations.  
- **Modular Updates**: Each parameter’s derivative depends only on its direct contribution to predictions.  

### **4.2 Simultaneous Optimization**  
- **Parallel Updates**: Adjust w3, w4, b3 together in each iteration.  
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
