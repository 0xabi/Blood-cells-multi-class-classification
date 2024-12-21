[![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white)](https://www.tensorflow.org/)
[![Keras](https://img.shields.io/badge/Keras-%23D00000.svg?style=for-the-badge&logo=Keras&logoColor=white)](https://keras.io/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)](https://matplotlib.org/)
[![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)](https://numpy.org/)



# Artificial Neural Network and Deep Learning
### Homework 1 - Blood Cells Multi Class Image Classification



## Table of Contents
- [Introduction](#-introduction)
- [Problem Analysis](#-problem-analysis)
- [Final model](#-final-model)
	- [Transfer learning](#-transfer-learning)
	- [Image data augmentation](#-image-data-augmentation)
	- [Optimizer and loss function](#-optimizer-and-loss-function)
- [Main experiments](#-main-experiments)
- [Conclusion](#-conclusion)
- [Contributors](#-contributors)


## Introduction
This study addresses a multi-class image classification problem using deep learning to classify 96x96
RGB images of blood cells into eight types, aiming to correctly label each image based on its features.

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/e1a65765-dc25-41fa-9693-0783032081aa" width="200"></td>
    <td><img src="https://github.com/user-attachments/assets/15b10723-eb73-4d93-b33e-d8cf227e66d8" width="200"></td>
    <td><img src="https://github.com/user-attachments/assets/d501516f-94b0-4909-a560-9b59bff8fc0e" width="200"></td>
    <td><img src="https://github.com/user-attachments/assets/cbd37fc9-7cf0-45bc-8f33-f8039bdacd46" width="200"></td>
  </tr>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/a2fe7f46-89cb-4b33-82de-375bf049b7dc" width="200"></td>
    <td><img src="https://github.com/user-attachments/assets/8c439fb8-bccc-4dd6-9d7a-24c6b11cb52b" width="200"></td>
    <td><img src="https://github.com/user-attachments/assets/e5f664b0-3344-4352-8584-65b86285a9e0" width="200"></td>
    <td><img src="https://github.com/user-attachments/assets/1aa4daab-ce5e-478d-a555-063bfc13e056" width="200"></td>
  </tr>
</table>










## Problem Analysis
We have to train several images but there were the following issues:
- **Class imbalance**: the unequal distribution of blood cell images posed a challenge for
the model, making it more difficult to learn the features of the underrepresented classes and potentially affecting its overall performance and ability to generalize effectively.

- **Limited variety in images**: the lack of diversity in visual features, such
as lighting conditions, orientations, and other factors, could prevent the model’s ability to generalize
and reduce its robustness on different scenarios and datasets.

- **Small dataset size**: it can lead to issues for achieving strong generalization and it can lead to overfit specific features.

## Final Model
### Transfer learning
The pre-trained models tested were **MobileNetV3Small**, **EfficientNetB0**, **EfficientNetV2S**,
**EfficientNetV2M** and **ConvNeXtBase**.

To improve results, some layers of the pre-trained models were **fine-tuned** using the **augmented**
training set created earlier.

Among the tested models, the one with the **ConvNeXtBase** pretrained network performed the best in this study.

### Image data agumentation
<p align="center"><strong>Figure 1: Data Augmentation Pipeline</strong></p>

![image](https://github.com/user-attachments/assets/34ed5769-c002-473c-8206-86a438da687f)

To ensure a balanced dataset, the number of images per class was increased to approximately 5500 using **ImageDataGenerator**
class from the Keras library, which allows augmentation by generating new images with slight geometric modifications.

The dataset was then passed through the pipeline illustrated in *Figure 1*, where random augmentation layers, taken from Keras CV
were applied to the training set.

The pipeline was selected by balancing two key objectives: enhancing generalization to improve model robustness and preserving image integrity to ensure representativeness of their respective classes.

### Optimizer and loss function
The Categotical Crossentropy loss function was employed with Lion optimizer.

## Main experiments
<p align="center"><strong>Table 1: Model’s results considering all main experiments that led to the best test score</strong></p>

| Model               | Train Accuracy / Val. Accuracy | Precision / Val. Precision | Recall / Val. Recall | AUC / Val. AUC | Online test Accuracy |
|---------------------|-------------------------------|----------------------------|----------------------|----------------|----------------------|
| CNN                 | 99.04/83.40                   | 99.07/83.34                | 99.04/83.40          | 100/95.24      | ≈ 0.23               |
| MobileNetV3Small    | 91.59/97.03                   | 95.24/95.24                | 88.60/96.57          | 99.36/99.86     | ≈ 0.43               |
| EfficientNetB0      | 46.68/69.69                   | 73.20/76.39                | 17.66/69.69          | 83.86/93.54     | ≈ 0.60               |
| EfficientNetV2S     | 75.91/93.23                   | 83.92/93.49                | 67.67/93.23          | 96.12/99.54     | ≈ 0.78               |
| EfficientNetV2M     | 76.51/96.34                   | 86.29/96.72                | 66.98/95.91          | 96.09/99.84     | ≈ 0.83               |
| **ConvNeXtBase**    | **81.91/96.95**               | **90.83/97.10**            | **74.56/96.73**      | **97.52/99.83** | ≈ **0.88**           |


## Conclusion
The best model, which has ConvNeXtBase achieved an accuracy of 88% on the provided testing set. \
The factors that had the most impact on the model's performance were **image augmentation** and the choice of the **pre-trained model**.

This trend suggests that enhancing the variety of training data through augmentation, along with using more sophisticated models, helps the model generalize better, resulting in higher performance on test datasets.

Further details are present in the report.

## Contributors
- [Sabrina Cesaroni](https://github.com/SabrinaCesaroni)
- [Samuele Vignolo](https://github.com/samuvignolo)
- [Mara Tortorella](https://github.com/maratortorella)
- [Abdullah Nasr](https://github.com/0xabi)
