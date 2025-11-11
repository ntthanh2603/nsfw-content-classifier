# Comprehensive Report: Comparison of Image Classification Models

## 1. Model Overview

This report summarizes and compares experimental results of four different image classification models:

1. **EfficientNet**
2. **ResNet34**
3. **Vision Transformer (ViT)**
4. **YOLOv8n**

## 2. Training Configuration Comparison

| Parameter             | EfficientNet                | ResNet34               | Vision Transformer | YOLOv8n                |
| --------------------- | --------------------------- | ---------------------- | ------------------ | ---------------------- |
| **Number of epochs**  | 15                          | 100                    | 100                | 10                     |
| **Learning rate**     | 0.001 (assumed)             | 0.1→0.01→0.001→0.0001  | 0.00001 (fixed)    | Increase-decrease schedule |
| **Special techniques** | Early stopping (patience=5) | Learning rate schedule | None               | Learning rate schedule |

## 3. Experimental Results Comparison

### 3.1. Highest Accuracy

| Model              | Highest Accuracy | On Dataset | Timing          |
| ------------------ | ---------------- | ---------- | --------------- |
| EfficientNet       | 97.04%           | Test       | Epoch 11 (best) |
| ResNet34           | 80.74%           | Test       | After 100 epochs |
| Vision Transformer | 74.81%           | Test       | After 100 epochs |
| YOLOv8n            | 95.9%            | Test       | Epoch 10        |

### 3.2. Loss Evolution

| Model              | Initial Loss | Final Loss | Characteristics                           |
| ------------------ | ------------ | ---------- | ----------------------------------------- |
| EfficientNet       | 0.0717       | 0.0583     | Irregular fluctuations from 0.0330-0.1081 |
| ResNet34           | 4.41         | 0.4341     | Decreases in LR phases, stable at end    |
| Vision Transformer | 1.073        | 0.0004     | Steady decrease, converges near 0        |
| YOLOv8n            | 0.83442      | 0.07431    | Fast decrease and stable                 |

### 3.3. Training Time and Performance

| Model              | Training Time        | Inference Performance | Fast Convergence           |
| ------------------ | -------------------- | -------------------- | -------------------------- |
| EfficientNet       | Not specified        | Not specified        | Achieves >92% from first epoch |
| ResNet34           | Not specified        | Not specified        | Slow loss decrease, stable |
| Vision Transformer | Not specified        | Not specified        | Steady loss decrease, final convergence |
| YOLOv8n            | Short (10 epochs)    | 17.4ms/image         | Achieves >90% after just 2 epochs |

## 4. Detailed Class-wise Analysis

### 4.1. EfficientNet Class-wise Metrics

| Class   | Precision | Recall | F1-score |
| ------- | --------- | ------ | -------- |
| Adult   | 1.0000    | 1.0000 | 1.0000   |
| Normal  | 0.9528    | 0.9712 | 0.9619   |
| Violent | 0.9595    | 0.9342 | 0.9467   |

### 4.2. EfficientNet Confusion Matrix

```
                        Predicted
                adult   normal violence
True    Adult       90        0        0
True   Normal        0      101        3
True  Violent        0        5       71
```

### 4.3. Other Models Metrics

- **ResNet34**: Only reports overall accuracy (80.74%), no detailed class-wise metrics
- **Vision Transformer**: Only reports overall accuracy (74.81%), no detailed class-wise metrics
- **YOLOv8n**: Reports Top-1 Accuracy (95.9%) and Top-5 Accuracy (100%)

## 5. Feature and Advantage Comparison

### 5.1. EfficientNet

- **Advantages**: Highest accuracy (97.04%), perfect classification for "Adult" class
- **Characteristics**: Validation accuracy fluctuates significantly, loss doesn't decrease evenly

### 5.2. ResNet34

- **Advantages**: Effective learning rate schedule
- **Characteristics**: Stable training, no sudden loss fluctuations

### 5.3. Vision Transformer

- **Advantages**: Training loss decreases to near 0 (0.0004)
- **Characteristics**: Low performance (74.81%) suggests possible overfitting

### 5.4. YOLOv8n

- **Advantages**: Fast convergence, high inference speed (17.4ms/image)
- **Characteristics**: High efficiency with few epochs (10)

## 6. Overall Performance Comparison

| Criteria                | EfficientNet       | ResNet34             | Vision Transformer | YOLOv8n            |
| ----------------------- | ------------------ | -------------------- | ------------------ | ------------------ |
| **Accuracy**            | ★★★★★ (97.04%)     | ★★★☆☆ (80.74%)       | ★★☆☆☆ (74.81%)     | ★★★★★ (95.9%)      |
| **Convergence speed**   | ★★★★☆ (15 epochs)  | ★★☆☆☆ (100 epochs)   | ★★☆☆☆ (100 epochs) | ★★★★★ (10 epochs)  |
| **Loss stability**      | ★★☆☆☆ (fluctuating) | ★★★★☆ (stable decrease) | ★★★★★ (steady decrease) | ★★★★☆ (fast decrease) |
| **Inference time**      | No information     | No information       | No information     | ★★★★★ (17.4ms/image) |
| **Overall rating**      | ★★★★★              | ★★★☆☆                | ★★☆☆☆              | ★★★★★              |

## 7. Conclusions and Recommendations

### 7.1. General Conclusions

From the experimental results of all four models, the following conclusions can be drawn:

1. **EfficientNet** and **YOLOv8n** are the two most effective models with >95% accuracy on test set, suitable for content-based image classification tasks.

2. **ResNet34** has moderate performance (80.74%) but stable training process, may need additional optimization.

3. **Vision Transformer** has the lowest performance (74.81%) on the MNIST dataset, suggesting that transformer architecture may not be suitable for simple data or needs hyperparameter adjustments.

4. **YOLOv8n** stands out with fast convergence capability (only 10 epochs) and high inference speed, suitable for practical applications and real-time processing.

### 7.2. Improvement Recommendations

#### For EfficientNet:

- Enhance data for "Normal" and "Violent" classes to reduce confusion
- Apply learning rate scheduler to stabilize training process

#### For ResNet34:

- Optimize learning rate schedule
- Apply additional regularization techniques (dropout, weight decay)
- Experiment with larger architectures (ResNet50, ResNet101)

#### For Vision Transformer:

- Apply regularization to avoid overfitting
- Experiment with learning rate schedule instead of fixed rate
- Adjust hyperparameters (number of layers, attention heads, patch size)

#### For YOLOv8n:

- Optimize dataset (increase number of hard samples)
- Adjust hyperparameters to reduce val loss fluctuation

### 7.3. Model Selection by Problem Type

- **Need highest accuracy**: EfficientNet (97.04%)
- **Need fast processing speed**: YOLOv8n (17.4ms/image)
- **Balanced practical application**: YOLOv8n (95.9% accuracy, 10 epochs, fast inference)
- **Complex data with many details**: ResNet34 with learning rate schedule
- **Complex spatial structure data**: Vision Transformer (after optimization)

## 8. Individual Model Reports

1. Analysis report of EfficientNet model for three-label image classification
2. Experimental results report of ResNet34 model
3. Experimental results report of Vision Transformer model
4. Performance analysis report of 16+ image classification project using YOLOv8n model

If you find any errors or areas for improvement, please don't hesitate to add an issue so the AI community can continue to grow :))
