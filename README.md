# GAYOGA

# Yoga Pose Image Classification using DenseNet

This project is an image classification model for yoga poses based on transfer learning techniques. The algorithm uses a pre-trained model to identify the coordinates of 17 keypoints in the image and produces new features based on the distance between the keypoints and their relative positions. A densely connected neural network is then trained on keypoint coordinates and position features to classify the image into one of 107 possible yoga poses.

# Pre-trained Models

The algorithm uses two pre-trained models provided by Google's TensorFlow Hub:

https://tfhub.dev/google/movenet/singlepose/thunder/3 - a larger model for higher accuracy
https://tfhub.dev/google/movenet/singlepose/lightning/3  - a smaller model for faster inference
Both models take an input of a frame of video or an image represented as an int32 tensor of shape:

256 x 256 x 3 for the larger model ("Thunder")
192 x 192 x 3 for the smaller model ("Lightning")
The channels order is RGB with values in the range of 0-255. The output is a float32 tensor of shape (1, 1, 17, 3). The first two channels of the last dimension represent the y and x coordinates normalized to the image frame, i.e., range in (0.0, 1.0) of the 17 keypoints 

# Densely Connected Neural Network
The algorithm uses a densely connected neural network with three hidden layers to classify the image into one of the 107 possible yoga poses. The model architecture is defined by the get_model function in the code. The n_features parameter is the number of input features, which is equal to 17 for the keypoint coordinates and 136 for the position features. The n_classes parameter is the number of output classes, which is 107. The dense_neurons parameter is a list of the number of neurons in each hidden layer, which is [256, 256, 128] in this case.

# Dataset

The dataset used to train and test this model consists of a collection of images of individuals performing 107 different yoga poses. The 17 keypoints identified by the algorithm are:

-> nose
-> left eye
-> right eye
-> left ear
-> right ear
-> left shoulder
-> right shoulder
-> left elbow
-> right elbow
-> left wrist
-> right wrist
-> left hip
-> right hip
-> left knee
-> right knee
-> left ankle
-> right ankle
These keypoints are used to classify the image into one of 107 possible yoga poses

![download](https://user-images.githubusercontent.com/102585626/236807878-a7e55e04-f524-42ad-9101-f434af2620a2.png)

# Training

The training progress of the model can be visualized using the training and validation loss and accuracy metrics. In the provided example, the model was trained for 100 epochs, and after 18 epochs, the training loss was 1.3583 and the training accuracy was 0.7266. The validation loss was 1.9982 and the validation accuracy was 0.6230 at this point.
![download](https://user-images.githubusercontent.com/102585626/236808805-f535414b-360a-4c4c-b2b3-8f174d16d057.png)

# Some potential areas for future work on this project include:

Adding additional layers to the model for further fine-tuning and optimization
Exploring alternative model architectures and training techniques to improve performance
Developing an application or platform for real-time yoga pose classification using this model.
