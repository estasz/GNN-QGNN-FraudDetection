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

This project is still WIP. Please note that the information will not always reflect the code present in GNN-QGNN.ipynb, as the code and results are being constantly updated. Feedback is welcome.

## Introduction

This project, by Erik Staszewski under the supervision of David Redmond for Equal1, seeks to implement and extend quantum computing techniques for credit card fraud detection. The primary objective is to construct and compare the performance of a classical Graph Neural Network (GNN) with a Quantum Graph Neural Network (QGNN) for binary classification of fraudulent and non-fraudulent credit card transactions.

Performance is evaluated using precision, recall, and $F_1$-scores, and plotted using Receiver Operating Characteristic (ROC) and Precision-Recall (PR) Curves.

<a name="top"></a>
<div align="center">
  <img src="./figures/benchmark.png" style="width: 60%;"/>
</div>

## Model Architecture

**GNN Model**

* Uses 3 GraphSAGE convolutional layers, each followed by batch normalization to stabilize training.
* Uses GeLU activation, enhancing non-linearity.
* The dense layer maps the embeddings to a single scalar output, followed by a sigmoid activation for binary fraud classification.
* Trained for 100 epochs, optimized using Adam with binary cross-entropy loss (BCELoss).

<a name="top"></a>
<div align="center">
  <img src="./figures/GNNarchitecture.png" style="width: 80%;"/>
</div>

**QGNN Model**

* Uses a hybrid quantum-classical approach, incorporating an SGConv layer for initial feature extraction.
* Quantum computation is performed with a single-qubit quantum layer, consisting of RX and RY gates, followed by pooling and a fully connected layer.
* Uses ReLU activation before the quantum layer to maintain expressiveness in classical feature extraction.
* Training uses gradient-based updates with the parameter shift rule, ensuring proper backpropagation through the quantum circuit.
* Trained for 200 epochs, optimized using Adam with binary cross-entropy loss (BCELoss).

<a name="top"></a>
<div align="center">
  <img src="./figures/QGNNarchitecture.png" style="width: 80%;"/>
</div>

## Results

<div align="center">

| Metric          | GNN (GraphSAGE) | QGNN (GCN) | QGNN (SGConv) |
|---------------|----------------|------------|---------------|
| Precision Score | 0.8645 | 0.8671 | 0.8662 |
| Recall Score | 0.8221 | 0.8405 | 0.8344 |
| $F_1$ Score | 0.8428 | 0.8536 | 0.8500 |
| ROC AUC | 0.9541 | 0.9237 | 0.9652 |
| PR AUC | 0.7843 | 0.7851 | 0.8076 |

</div>

The charts below compare the GNN (GraphSAGE) and QGNN (SGConv) models. SGConv was selected as the preferred QGNN architecture because it outperformed GNN across all five metrics, while GCN outperformed the classical GNN in only four metrics.
