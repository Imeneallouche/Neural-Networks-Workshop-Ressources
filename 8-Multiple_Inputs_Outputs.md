# Neural Networks Part 4 – Multiple Inputs and Outputs  

## **1. Introduction to Multi-Input/Output Networks**  
Neural networks can handle **multiple inputs** (e.g., petal and sepal widths) and **multiple outputs** (e.g., iris species classification). This lesson demonstrates how neural networks process multi-dimensional data to create complex decision boundaries ("crinkled surfaces") for predictions.  

---

## **2. Neural Network Architecture**  

### **2.1 Input Layer**  
- **Inputs**:  
  - **Petal Width**: Scaled between 0 (smallest) and 1 (largest).  
  - **Sepal Width**: Scaled similarly.  
- **Purpose**: Predict iris species (Setosa, Versicolor, Virginica).  

### **2.2 Hidden Layer**  
- **Nodes**:  
  - Each node applies **ReLU activation** to inputs.  
  - **Example**:  
    - Top Node: \( x_{\text{top}} = (\text{Petal} \times -2.5) + (\text{Sepal} \times 0.6) + 1.6 \).  
    - Apply ReLU: \( \text{ReLU}(x_{\text{top}}) = \max(0, x_{\text{top}}) \).  

### **2.3 Output Layer**  
- **Outputs**:  
  - **Setosa**, **Versicolor**, **Virginica** (each with separate output nodes).  
- **Final Activation**: Optional (e.g., Softmax for classification).  

---

## **3. Forward Pass: From Inputs to Predictions**  

### **3.1 Single Output (Setosa Example)**  
1. **Inputs**: Petal width = 0, Sepal width = 0.  
2. **Hidden Layer**:  
   - Top Node: \( x_{\text{top}} = 1.6 \rightarrow \text{ReLU}(1.6) = 1.6 \).  
   - Bottom Node: Similar calculations.  
3. **Combine Hidden Outputs**:  
   - Multiply by weights (e.g., -0.1 for blue surface, 1.5 for orange surface).  
   - Add outputs: \( -0.16 + 1.05 = 0.89 \).  
4. **Final Prediction**: Setosa score = 0.89 (closer to 1 → likely Setosa).  

### **3.2 Multiple Outputs (All Species)**  
- **Versicolor**: Hidden outputs scaled by 2.4 and -5.2 → Red crinkled surface.  
- **Virginica**: Hidden outputs scaled by -2.2 and 3.7 → Purple crinkled surface.  

---

## **4. Visualizing Decision Surfaces**  

### **4.1 3D Graphs**  
- **Axes**:  
  - **X**: Petal Width (0–1).  
  - **Y**: Sepal Width (0–1).  
  - **Z**: Prediction Score (0–1).  
- **Surfaces**:  
  - **Blue/Orange Bent Surfaces**: Outputs from hidden nodes.  
  - **Crinkled Surfaces**: Combined outputs (e.g., green for Setosa, red for Versicolor).  

### **4.2 Interpretation**  
- **High Scores**: Indicate higher probability of a species.  
  - Example: Petal width ≈ 1 → High Virginica score.  

---

## **5. Practical Example: Predicting Iris Species**  

### **5.1 Input Values**  
- **Petal Width**: 0.5 (scaled).  
- **Sepal Width**: 0.37 (scaled).  

### **5.2 Prediction**  
1. **Setosa**: Score = 0.09 (low).  
2. **Versicolor**: Score = 0.86 (high).  
3. **Virginica**: Score = TBD (likely low).  
- **Result**: Likely Versicolor (closest to 1).  

---

## **6. Key Concepts**  

### **6.1 Argmax vs. Softmax**  
- **Argmax**: Selects output node with the highest score (used here).  
- **Softmax**: Converts scores into probabilities (covered in future lessons).  

### **6.2 Scaling Inputs**  
- **Why?**: Ensures consistent training (e.g., 0–1 scaling).  
- **Note**: 0 ≠ absolute minimum; it reflects the smallest value in the dataset.  

---

## **7. Summary**  
Neural networks with multiple inputs/outputs:  
1. Process inputs through **hidden layers** (ReLU activation).  
2. Combine outputs into **3D surfaces** for predictions.  
3. Use **argmax** or **softmax** to finalize decisions.  
This architecture enables complex tasks like multi-class classification (e.g., iris species).  
