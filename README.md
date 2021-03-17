# Artificial Neural Network and Deep Learning Competition
*Artificial Neural Network and Deep Learning* is a course offered by Politecnico di Milano for the first time in the acedemic year 2019/2020 (first semester).
In this repository you can find the *Jupyter Notebooks* used by me and a colleague of mine to partecipate at the competition in that academic year (2019/2020).

The competition was divided into three challenges, each one of them cover a different topic of the course:
 - Image Classification 
 - Image Segmentation
 - Visual Question Answering

## 1. Image Classification
[![open-Kaggle](https://img.shields.io/badge/open-Kaggle-4791CD.svg)](https://www.kaggle.com/c/ann-and-dl-image-classification)

The goal of this competition was to build a multiclass classifier to solve an Image Classification problem.

Details:
 - 20 different classes (e.g. kangaroo, owl, mountain-bike, waterfall, galaxy, ...)
 - 1554 images in training set (with different dimension)
 - 500 images for testing
 - **Evaluation**: Multiclass Accuracy

<p align="center">
    <img src="https://i.imgur.com/sEpZYci.jpg" width="500" alt="Scenario"/>
</p>

*Best result*: 98.4% of accuracy. In order to reach that performance we take all the images of the training set and we resized them to a fixed dimension, then we augmented them in order to have more samples for each class. The final model exploits transfer learning using a InceptionResNet v2 with pretrained weights from Imagenet and to improve further the accuracy, we unfroze the last layers in order to modify them a little bit, sufficiently to reach out best performance.

## 2. Image Segmentation
[![open-Kaggle](https://img.shields.io/badge/open-Kaggle-4791CD.svg)](https://www.kaggle.com/c/ann-and-dl-image-segmentation)

In this case the goal was to solve a Segmentation problem: the dataset contains aerial images of different areas and the goal is to segment buildings at pixel level, thus predicting for each pixel if it belongs to a building (class 1) or not (class 0), creating a mask that represent the buildings.

<p align="center">
    <img src="https://i.imgur.com/dPF8QEH.png" width="500" alt="Scenario"/>
</p>

Details:
 - Satellite building images, binary segmentation (background/building)
 - 7647 images in training set (size: 256x256)
 - 1234 for testing
 - **Evaluation**: IoU, Insertion over Union

*Best result*: of 0.52 of IoU. To achieve this result we first applied data augmentation and then we use a UNet shaped model with batch normalization in order to have encoding-decoding of data, that is the correct way to solve segmentation problems.

## 3. Visual Question Answering
[![open-Kaggle](https://img.shields.io/badge/open-Kaggle-4791CD.svg)](https://www.kaggle.com/c/ann-and-dl-vqa)

In this last competition the goal was to solve a Visual Question Answering (VQA) problem on the proposed dataset, which contains synthetic scenes composed by several objects and corresponding questions about the existence of something in the scene (e.g., Is there a yellow thing?') or about counting (e.g., How many big objects are there?').

Given an image and a question, the goal is to provide the correct answer.

<p align="center">
    <img src="https://i.imgur.com/uDgrQt0.png" width="700" alt="Scenario"/>
</p>

Details:
 - *input*: an image and a question about the image
 - *output*: answer to the question. **13 possible answer**: numbers from 0 to 10, 'yes' and 'no'. It's treated as a classification problem (the class is the answer)
 - 259492 questions in training set (two type of questions: "exists" or "count")
 - 69642 images in training set (size: 320x480)
 - 3000 questions for testing
 - 2754 images for testing
 - **Evaluation**: Multiclass Accuracy

*Best result*: 28.1% of accuracy. We first built a data generator to solve the problem of fitting the images in memory. Then we read the questions from the json file and tokenized them. The final model consists in the collaboration between a convolutional neural network (CNN) based on VGG and a bidirectional recurrent network, concatenated thanks to a final dense part.
