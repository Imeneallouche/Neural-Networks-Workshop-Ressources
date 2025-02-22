# Cross-Entropy Derivatives and Backpropagation  

## **1. Introduction**  
**Cross-entropy** is a critical loss function for classification tasks in neural networks. This lesson demonstrates how to compute its derivatives and apply **backpropagation** to optimize parameters like bias terms. Using an iris species classification example, we focus on adjusting the bias \( b_3 \) to minimize loss.  

---

## **2. Forward Pass and SoftMax Activation**  

### **2.1 Neural Network Architecture**  
- **Inputs**: Petal and sepal widths (scaled between 0 and 1).  
- **Hidden Layers**: Generate "bent surfaces" via ReLU activation.  
- **Output Layer**: Combines surfaces with weights/biases to create "crinkled surfaces" for each class (Setosa, Versicolor, Virginica).  

### **2.2 SoftMax Activation**  
Raw outputs (\( z \)) from the final layer are converted to probabilities:  
\[
\text{SoftMax}(i) = \frac{e^{z_i}}{\sum_{j=1}^3 e^{z_j}}  
\]  
**Example**: For Setosa:  
\[
\text{Predicted Probability (Setosa)} = \frac{e^{z_{\text{Setosa}}}}{e^{z_{\text{Setosa}}} + e^{z_{\text{Versicolor}}} + e^{z_{\text{Virginica}}}}  
\]  

---

## **3. Cross-Entropy Loss**  
For a single observation with true class \( i \):  
\[
\text{Cross-Entropy} = -\log(\text{Predicted Probability for } i)  
\]  
**Example**: If the true class is **Setosa** and its predicted probability is 0.57:  
\[
\text{Loss} = -\log(0.57) \approx 0.56  
\]  

---

## **4. Derivative of Cross-Entropy with Respect to Bias \( b_3 \)**  

### **4.1 Chain Rule Breakdown**  
To optimize \( b_3 \), compute:  
\[
\frac{\partial \text{Cross-Entropy}}{\partial b_3} = \frac{\partial \text{Cross-Entropy}}{\partial \text{Predicted Probability}} \cdot \frac{\partial \text{Predicted Probability}}{\partial z_{\text{Setosa}}} \cdot \frac{\partial z_{\text{Setosa}}}{\partial b_3}  
\]  

#### **Step 1: Derivative of Cross-Entropy w.r.t. Predicted Probability**  
\[
\frac{\partial \text{Cross-Entropy}}{\partial \text{Predicted Probability}} = -\frac{1}{\text{Predicted Probability}}  
\]  

#### **Step 2: Derivative of SoftMax w.r.t. Raw Output \( z_{\text{Setosa}} \)**  
\[
\frac{\partial \text{SoftMax(Setosa)}}{\partial z_{\text{Setosa}}} = \text{SoftMax(Setosa)} \cdot (1 - \text{SoftMax(Setosa)})  
\]  

#### **Step 3: Derivative of Raw Output \( z_{\text{Setosa}} \) w.r.t. \( b_3 \)**  
\[
\frac{\partial z_{\text{Setosa}}}{\partial b_3} = 1 \quad (\text{since } z_{\text{Setosa}} = \text{Hidden Outputs} + b_3)  
\]  

#### **Final Derivative for Setosa Observation**:  
\[
\frac{\partial \text{Cross-Entropy}}{\partial b_3} = (\text{SoftMax(Setosa)} - 1)  
\]  

### **4.2 Example Calculation**  
- If \( \text{SoftMax(Setosa)} = 0.15 \):  
\[
\frac{\partial \text{Cross-Entropy}}{\partial b_3} = 0.15 - 1 = -0.85  
\]  

---

## **5. Derivatives for Other Classes**  

### **5.1 Observed Class = Virginica**  
The derivative involves the **predicted probability of Setosa** due to the softmax denominator:  
\[
\frac{\partial \text{Cross-Entropy}}{\partial b_3} = \text{SoftMax(Setosa)}  
\]  
**Example**: If \( \text{SoftMax(Setosa)} = 0.04 \):  
\[
\frac{\partial \text{Cross-Entropy}}{\partial b_3} = 0.04  
\]  

### **5.2 Observed Class = Versicolor**  
Same as Virginica:  
\[
\frac{\partial \text{Cross-Entropy}}{\partial b_3} = \text{SoftMax(Setosa)}  
\]  

---

## **6. Gradient Descent Update**  

### **6.1 Total Derivative Across Observations**  
Sum derivatives for all training examples:  
\[
\frac{\partial \text{Total Cross-Entropy}}{\partial b_3} = \sum (\text{Derivatives per Observation})  
\]  

**Example**:  
- Three observations with derivatives: \(-0.85\), \(0.04\), \(0.04\)  
\[
\text{Total Derivative} = -0.85 + 0.04 + 0.04 = -0.77  
\]  

### **6.2 Update Rule**  
\[
b_3^{\text{new}} = b_3^{\text{old}} - (\text{Learning Rate} \times \text{Total Derivative})  
\]  
**Example**:  
- \( b_3^{\text{old}} = -2 \), Learning Rate = 1:  
\[
b_3^{\text{new}} = -2 - (1 \times -0.77) = -1.23  
\]  

---

## **7. Key Takeaways**  
1. **Cross-Entropy Derivatives**: Depend on the observed class and predicted probabilities.  
2. **Bias Optimization**: Adjusting \( b_3 \) shifts the "crinkled surface" to better fit the data.  
3. **Generalization**: The same process applies to other parameters (e.g., \( w_3 \), \( b_4 \)).  

## **8. Summary**  
- **Cross-Entropy** provides gradients that guide parameter updates during backpropagation.  
- Derivatives for biases involve the chain rule and softmax probabilities.  
- Gradient descent iteratively minimizes loss by adjusting parameters like \( b_3 \).  
