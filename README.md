
-![subfury](https://github.com/user-attachments/assets/e1328a64-077f-47df-bf2d-da588bbe9a79)
--

# **SubFury: AI-Powered Subdomain Prediction & Enumeration System** 

**SubFury** is an AI-driven platform designed to revolutionize subdomain enumeration using **NLP** and **machine learning**. By leveraging **DistilGPT-2** and incorporating **reinforcement learning**, SubFury predicts potential subdomains and validates them in real-time with advanced DNS resolution techniques.

Whether you're a **pentester**, **red teamer**, or **cybersecurity researcher**, SubFury empowers you with a smarter, more efficient subdomain discovery process. 🚀

---

## 🌟 **Key Features**

- **AI-Powered Subdomain Prediction**: Utilizes **DistilGPT-2** for predicting subdomains.
- **DNS Validation**: Validates predictions with real-time **DNS resolution**.
- **Reinforcement Learning**: Continuously improves through feedback from DNS results.
- **Efficient Resource Management**: Smart checkpointing and mixed precision to optimize memory, disk space, and GPU usage.
- **W&B Integration**: Real-time monitoring with **Weights & Biases**.

---

## 🔍 **Workflow Overview**

1. **Dataset Collection**: SubFury uses the **n0kovo_subdomains** dataset.
2. **Preprocessing**: Tokenization prepares the data for input into **DistilGPT-2**.
3. **Model Training**: The model learns subdomain patterns from the dataset.
4. **Subdomain Prediction**: SubFury generates potential subdomains using the trained model.
5. **DNS Validation**: Real-time DNS lookups validate the predictions.
6. **Reinforcement Learning**: The model improves based on feedback from successful or failed DNS resolutions.
7. **Continuous Learning**: The model is periodically retrained to adapt to new patterns.

---

## 🤔 **Why Choose DistilGPT-2?**

**DistilGPT-2** strikes the balance between power and efficiency:

- **Lightweight** yet capable of understanding complex patterns.
- **Pretrained** on large datasets for strong foundational knowledge.
- **Fast and memory-efficient**, ideal for subdomain enumeration tasks.

---

## 🧠 **Training the Model**

We fine-tuned **DistilGPT-2** on the **n0kovo_subdomains** dataset. Here’s a summary of the training setup:

- **Batch Size**: `per_device_train_batch_size=8`
- **Epochs**: `num_train_epochs=5`
- **Checkpointing**: Only the last 2 checkpoints are saved (`save_total_limit=2`).
- **Mixed Precision**: Used to speed up training and reduce memory usage (`fp16=True`).
- **Real-time Monitoring**: Tracked using **Weights & Biases (W&B)** for detailed insights.

### 🎯 **Training Process**

1. **Fine-Tuning**: We trained the model to predict subdomains based on common patterns in the **n0kovo_subdomains** dataset.
2. **DNS Validation**: After prediction, subdomains are validated through real-time DNS resolution.
3. **Reinforcement Learning**: The model refines its predictions by learning from validation feedback.

---

## 🌐 **DNS Validation (Sample)**

After training, SubFury generates subdomain predictions, which are validated using DNS resolution. Here’s a simple validation function:

```python
import socket

def dns_resolve(subdomain):
    try:
        ip = socket.gethostbyname(subdomain)
        return subdomain, ip
    except socket.gaierror:
        return subdomain, None
```

This is a sample DNS resolution—more advanced techniques are applied for real-world results.

---

## 🔄 **Reinforcement Learning**

SubFury uses **reinforcement learning** to improve continuously:

- **Positive Reward**: When a predicted subdomain resolves successfully.
- **Negative Reward**: When the subdomain fails to resolve.

The model adapts over time, prioritizing patterns that lead to valid subdomains.

---

## 📊 **Monitoring & Reporting**

SubFury tracks the training and validation process using **Weights & Biases**:

- **Training Loss**: Monitored throughout the process.
- **GPU Utilization**: Keeps track of system resources.
- **DNS Success Rate**: Monitors how many predicted subdomains are successfully resolved.

---

## 📈 **Workflow Diagram**

```plaintext
      +-------------------------+      +--------------------------+      +-------------------------+
      | Subdomain Dataset        |      | Tokenization & Encoding   |      | Subdomain Prediction     |
      | (n0kovo_subdomains)      +----->| (GPT-2 Positional Encoding)+----->| Using GPT-2 Model        |
      +-------------------------+      +--------------------------+      +-------------------------+
                                                                         |
                                                                         v
                                                               +--------------------------+
                                                               | DNS Validation & Feedback |
                                                               | (Real-Time Resolution)    |
                                                               +--------------------------+
                                                                         |
                                                                         v
                                                               +--------------------------+
                                                               | Reinforcement Learning    |
                                                               | (Positive/Negative Rewards)|
                                                               +--------------------------+
                                                                         |
                                                                         v
                                                               +--------------------------+
                                                               | Continuous Learning       |
                                                               | (Fine-Tuning & Updates)   |
                                                               +--------------------------+
```

---

## 📝 **License**

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for more details.

---
