Dataset Analysis and Preprocessing
Data Preprocessing
Initially, I conducted a brief statistical analysis. Specifically, I examined the number of images per class and found that some classes were underrepresented, with image counts ranging from 34 to over 500. To address this, I considered balancing the dataset to ensure more robust learning by the model.

Before making these adjustments, I extracted 30% of the images from each label for validation. To balance the training set, I increased the number of images for underrepresented classes to 300 by randomly duplicating them. This process intensively affected only a few classes, particularly one, while the others underwent minor duplication to reach 300. After this process, I had a training set of 85,788 images and a validation set of 35,543 images. I believed it was better for the model to overfit on the same images rather than underfit and fail to make correct predictions. Overfitting was slightly mitigated through data augmentation, ensuring the model did not see the same images but different versions of them in each epoch.

Data augmentation was performed by flipping images horizontally, applying shear transformations, and using random resized crops. Specifically, shear transformations slide parts of an image along an axis, while random resized crops involve changing the size of an image and then cutting out a random part of it.

Task Implementation and Evaluation
Structure of the NN
The Convolutional Neural Network was constrained to have less than one million parameters. I chose a CNN and will explain the reasoning behind this choice.

The idea was to take inspiration from an existing neural network to have an optimal starting point. Therefore, I considered MobileNetV2, which was not suitable for my problem since it had over three million parameters and its linear classifier provided classification over one thousand classes. First, I modified the linear classifier to have an output of 251. Then I adjusted the number of neurons, modifying them and cutting layers to reach my goal of having fewer than one million parameters. Finally, I achieved a model with 999,928 parameters.

I want to highlight that I made this choice because I planned to use the transfer learning method as an additional way to improve the accuracy achievable by the network. This will be further developed in another section. The weights were not specifically initialized, so they were sampled from a uniform distribution, the default one.

Inverted Residual Blocks
The MobileNet network is designed to be particularly fast and implemented for devices with limited computational capabilities. The idea behind this neural network is to use a variant of the Standard Convolution, which is less computationally expensive. The authors of the paper I referenced introduced the so-called Depthwise Convolution, which breaks the convolution into two steps.

The first step performs the convolution only on a single channel, meaning that there is one kernel per channel, and it is applied only to the associated channel. The second step is the mixing phase, where a 1x1 kernel convolution is applied to work across different channels.

The core idea is the concept of the Manifold of Interest, which suggests that pixels and their feature vectors actually reside in a low-dimensional space. Therefore, the objective is to project them into that space without losing too much information. The result of this idea is the Linear Bottleneck, which aims to reduce dimensionality while preserving the manifold structure.

This leads to layers known as Inverted Residuals. These consist of three phases: Expansion, Depthwise Convolution, and Linear Projection. Expansion involves increasing pixel dimensionality to reach a high-dimensional space. After performing the depthwise convolution, the dimensionality is reduced through a linear projection map. This last operation does not have any activation function. Additionally, if the input and output have the same size, a skip connection is added. This helps to avoid the vanishing gradient problem.

Training
I reported notable training parameters, including a learning rate of 0.001, the Adam optimizer, and the CosineAnnealingLR scheduler. I trained the model for 60 epochs with a batch size of 100 and implemented early stopping. If the validation loss did not improve for more than three consecutive epochs, training was halted, and the best model was saved.

I did not use weight decay or dropout in the classifier. I believed that data augmentation and the early stopping procedure would be enough to prevent overfitting.

Results
After training, I evaluated the model on the validation set. The model achieved a validation accuracy of 36.63% after 40 epochs before early stopping occurred. Although the accuracy is quite low, given the constraints on the number of parameters, I considered it a good achievement.

SSL (Semi-Supervised Learning)
In this part, I implemented semi-supervised learning. The method involves training the model on a small portion of data to complete a task not directly related to the ultimate goal but necessary for the model to extract features needed for the actual aim.

The Choice of the Task
First Reasoning
It was crucial to choose the correct task for the model, adapting it according to the given datasets. Initially, I experimented with the code developed during lessons. The provided task involved predicting rotations: an image is rotated and labeled with the rotation done (out of four possibilities), and the model is trained to predict the current rotation. However, the accuracy did not exceed 2% after more than 5 epochs. This led me to consider two aspects. First, most food images are taken from above, so rotating them does not make much difference. Second, since data augmentation often involves rotations, this can create conflicts in semi-supervised learning.

Second Reasoning
Due to these issues, I switched to a puzzle-based task. Each image is divided via a 3x3 grid, resulting in 9 blocks that are then shuffled, with positions saved as the "ground truth." During training, batches of images are divided into these blocks, each of which is passed to the neural network, which is supposed to predict its correct position.

Even this task did not yield the expected results. The model learned to correctly classify the puzzles, achieving a validation accuracy of 76.67%. But the actual task reached a poor 0.84%.

I believe that the task was not challenging enough to help the model learn important features and textures, or there were mistakes in the code that I haven't found yet.

Transfer Learning
I implemented the transfer learning method by initializing the neural network with weights pretrained on the ImageNet dataset to see if this could improve performance compared to the previous initialization.

Results
The training was carried out for 26 epochs before early stopping occurred, and the model achieved a final validation accuracy of 37.61%. The results are still quite low, but given the constraints, I am satisfied.
