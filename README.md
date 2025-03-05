<!-- markdownlint-disable first-line-h1 -->
<!-- markdownlint-disable html -->
<!-- markdownlint-disable no-duplicate-header -->

<a name="top"></a>
<div align="center">
  <img src="./figures/equal1.png" style="width: 300px;"/>
</div>

---

<div align="center">
   <a href="mailto:erik.staszewski@gmail.com"><b>Email Me</b></a> | <a href="https://www.linkedin.com/in/estaszewski/"><b>My LinkedIn</b></a></b></a> | <a href="https://www.equal1.com/"><b>Equal1 Website</b></a></b></a>
</div>

This project is still WIP. Please note that the information presented below may not always reflect the code present in GNN-QGNN.ipynb, as the code and results are being constantly updated. Feedback is welcome.

## Introduction

This project, by Erik Staszewski under the supervision of David Redmond for Equal1, seeks to implement and extend quantum computing techniques for credit card fraud detection. The primary objective is to construct and compare the performance of a classical Graph Neural Network (GNN) with a Quantum Graph Neural Network (QGNN) for binary classification of fraudulent and non-fraudulent credit card transactions.

Performance is evaluated using precision, recall, and $F_1$-scores, and plotted using Receiver Operating Characteristic (ROC) and Precision-Recall (PR) Curves.

<a name="top"></a>
<div align="center">
  <img src="./figures/benchmark.png" style="width: 60%;"/>
</div>

## Model Architecture

**GNN Model**

* The model consists of 3 GraphSAGE convolutional layers, each followed by batch normalization to stabilize training, and GeLU activation to enhance non-linearity.
* A fully connected (dense) layer maps the final embeddings to a single scalar output, followed by a sigmoid activation for fraud classification.
* The model is trained for 100 epochs, optimized using Adam, with BCELoss (or FocalLoss) as the loss function, and a learning rate of 0.01.

<a name="top"></a>
<div align="center">
  <img src="./figures/GNNarchitecture.png" style="width: 80%;"/>
</div>

**QGNN Model**

* This model uses a hybrid quantum-classical approach, starting with an SGConv layer for feature extraction, followed by ReLU activation.
* A single-qubit quantum layer is used, implementing RX and RY gates, followed by pooling and a fully connected layer.
* The model is trained for 200 epochs, optimized using Adam, with BCELoss (or FocalLoss) as the loss function, and a learning rate of 0.01.

<a name="top"></a>
<div align="center">
  <img src="./figures/QGNNarchitecture.png" style="width: 80%;"/>
</div>

## Results

<div align="center">

| Metric          | GNN (GCN) | GNN (GraphSAGE) | QGNN (GCN) | QGNN (SGConv) |
|---------------|----------------|----------------|------------|---------------|
| Precision Score | 0.8627 | 0.8645 | **0.8671** | 0.8662 |
| Recall Score | 0.8098 | 0.8221 | **0.8405** | 0.8344 |
| $F_1$ Score | 0.8354 | 0.8428 | **0.8536** | 0.8500 |
| ROC AUC | **0.9659** | 0.9541 | 0.9237 | 0.9652 |
| PR AUC | 0.7490 | 0.7843 | 0.7851 | **0.8076** |

</div>

Values in **bold** indicate the best results in that metric.
