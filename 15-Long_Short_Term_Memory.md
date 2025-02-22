# Long Short-Term Memory (LSTM) Networks

## **1. Introduction to LSTMs**  
**Why LSTMs?**  
Traditional RNNs struggle with **long-term dependencies** due to vanishing/exploding gradients. LSTMs solve this by:  
1. Separating **long-term memory** (cell state) and **short-term memory** (hidden state).  
2. Using **gating mechanisms** to regulate information flow.  

---

## **2. Core Components of LSTMs**  

### **2.1 The Cell State and Hidden State**  
- **Cell State (Long-Term Memory)**:  
  - A "highway" that carries information across time steps with minimal transformations.  
  - Avoids vanishing/exploding gradients by using **additive updates** instead of multiplicative.  
- **Hidden State (Short-Term Memory)**:  
  - Outputs information to the next time step and influences predictions.  

### **2.2 The Three Gates**  
| **Gate**       | **Function**                                                                 | **Activation** |  
|-----------------|-----------------------------------------------------------------------------|----------------|  
| **Forget Gate** | Decides what to discard from the cell state.                                | Sigmoid (0–1)  |  
| **Input Gate**  | Decides what new information to store in the cell state.                    | Sigmoid + Tanh |  
| **Output Gate** | Decides what to output from the cell state to the hidden state.             | Sigmoid + Tanh |  

---

## **3. Step-by-Step: How LSTMs Work**  

### **3.1 Forget Gate**  
1. **Inputs**: Previous hidden state (h{t-1}) and current input (xt).  
2. **Operation**:  
   \[
   f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)
   \]  
   - \( f_t \) (forget vector) determines what to remove from the cell state (\( C_{t-1} \)).  

### **3.2 Input Gate**  
1. **Candidate Memory**:  
   \[
   \tilde{C}_t = \tanh(W_C \cdot [h_{t-1}, x_t] + b_C)
   \]  
   - Generates potential updates using **tanh** (-1 to 1).  
2. **Update Vector**:  
   \[
   i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i)
   \]  
   - \( i_t \) (input vector) decides how much of \( \tilde{C}_t \) to add to \( C_t \).  

3. **Update Cell State**:  
   \[
   C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t
   \]  
   - \( \odot \): Element-wise multiplication.  

### **3.3 Output Gate**  
1. **Output Vector**:  
   \[
   o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o)
   \]  
2. **New Hidden State**:  
   \[
   h_t = o_t \odot \tanh(C_t)
   \]  
   - Combines filtered cell state and output gate to produce the hidden state.  

---

## **4. Example: Stock Price Prediction**  

### **4.1 Scenario**  
- **Companies A & B**: Stock values differ only on Day 1 (A=0, B=1) and Day 5 (A=0, B=1).  
- **Goal**: Predict Day 5 values using Days 1–4.  

### **4.2 LSTM in Action**  
1. **Day 1**:  
   - **Company A**: Input=0 → Cell state updated to retain "0".  
   - **Company B**: Input=1 → Cell state updated to retain "1".  
2. **Days 2–4**:  
   - Both companies input=0.5 → LSTM retains prior cell state (0 or 1).  
3. **Day 5**:  
   - **Output**: Company A=0, Company B=1.  
   - **Mechanism**: Cell state preserves critical Day 1 information through gates.  

---

## **5. Why LSTMs Avoid Gradient Issues**  
- **Cell State Design**: Additive updates

![image](https://github.com/user-attachments/assets/09526ad8-dbc2-440f-8897-ece5dc2b6f25)

   prevent multiplicative gradient decay/explosion.  
- **Gating**: Sigmoid (0–1) and tanh (-1–1) regulate information flow, stabilizing gradients during backpropagation.  

---

## **6. Key Takeaways**  
1. **Long-Term Memory**: Cell state retains critical information over long sequences.  
2. **Gates**:  
   - **Forget Gate**: Filters irrelevant past information.  
   - **Input Gate**: Adds relevant new information.  
   - **Output Gate**: Decides what to pass to the next time step.  
3. **Applications**: Time-series prediction, NLP, speech recognition.  

---

## **7. Summary**  
LSTMs overcome RNN limitations by:  
1. Separating long/short-term memory.  
2. Using gated mechanisms to control information flow.  
3. Stabilizing gradients for training on long sequences.  
