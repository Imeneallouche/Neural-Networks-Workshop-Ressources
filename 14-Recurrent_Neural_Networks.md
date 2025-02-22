# Recurrent Neural Networks (RNNs)

## **1. Introduction to RNNs**  
**Why RNNs?**  
Traditional neural networks struggle with **sequential data** (e.g., time series, text) because they:  
- Require fixed input sizes.  
- Ignore temporal dependencies (relationships between data points over time).  

**RNNs solve these issues** by:  
1. **Handling variable-length sequences**.  
2. Using **feedback loops** to retain memory of previous inputs.  
3. Sharing weights across time steps for efficiency.  

---

## **2. Core Components of RNNs**  

### **2.1 Feedback Loop**  
- **Key Feature**: Hidden layer outputs are fed back into the network as inputs for the next time step.  
- **Purpose**: Maintain a "memory" of past information.  

### **2.2 Unrolling the Network**  
- **Process**: Convert the feedback loop into sequential copies of the network.  
  - Example: For 3 days of stock data, unroll the RNN into 3 time steps.  
- **Shared Weights**: The same weights W1, W2 ) and biases ( b1 ) are reused across all time steps.  

---

## **3. Step-by-Step: Predicting Stock Prices in StatLand**  

### **3.1 Example Setup**  
- **Goal**: Predict tomorrow’s stock price using yesterday’s and today’s prices.  
- **Data**:  
  - Low = 0, Medium = 0.5, High = 1.  
  - Patterns:  
    - Two low days → Tomorrow low.  
    - Low → Medium → Tomorrow high.  
    - High → Medium → Tomorrow low.  

### **3.2 Forward Pass**  
1. **Input**: Yesterday’s value (t-1) → Process through the RNN.  
2. **Feedback**: Hidden state (Y1) is passed to the next time step.  
3. **Next Input**: Today’s value (t) combines with Y1.  
4. **Output**: Predict tomorrow’s value (t+1).  

**Example**:  

![image](https://github.com/user-attachments/assets/84b61755-e3d5-4715-9ab8-95a2be6b525b)


---

## **4. Key Concepts**  

### **4.1 Shared Parameters**  
- **Weights W1, W2** and **biases b1** are reused across all unrolled time steps.  
- **Benefit**: Reduces the number of parameters, making training feasible.  

### **4.2 Vanishing/Exploding Gradients**  
- **Cause**: Repeated multiplication of weights during backpropagation through time (BPTT).  
  - **Exploding Gradients**: W2 > 1 → Gradients grow exponentially (e.g., 2^{50}).  
  - **Vanishing Gradients**: W2 < 1 → Gradients shrink to near-zero (e.g., 0.5^{50}).  
- **Impact**:  
  - Exploding: Unstable training (overshooting optimal parameters).  
  - Vanishing: Slow/no convergence (tiny updates).  

### **4.3 Solutions**  
- **Long Short-Term Memory (LSTM)**: Uses gating mechanisms to control information flow.  
- **Gradient Clipping**: Limit gradient magnitudes during training.  

---

## **5. Advantages and Limitations**  

| **Advantages**                          | **Limitations**                          |  
|-----------------------------------------|------------------------------------------|  
| Handles variable-length sequences.      | Struggles with long-term dependencies.   |  
| Captures temporal patterns.             | Prone to vanishing/exploding gradients.  |  
| Efficient parameter sharing.            | Computationally intensive for long sequences. |  

---

## **6. Practical Example**  

### **6.1 Three Days of Data**  
- **Unrolling**: Expand the RNN into 3 time steps (day t-2, t-1, t).  
- **Prediction**: Final output at t+1 uses all prior hidden states.  

### **6.2 Training with Backpropagation**  
1. **Forward Pass**: Compute predictions for all time steps.  
2. **Loss Calculation**: Compare predictions to true values (e.g., sum of squared residuals).  
3. **Backward Pass**: Compute gradients and update weights.  

---

## **7. Summary**  
- **RNNs** excel at processing sequential data by maintaining memory through feedback loops.  
- **Unrolling** allows handling of variable-length inputs.  
- **Vanishing/Exploding Gradients** are major challenges, addressed by techniques like **LSTMs**.  
