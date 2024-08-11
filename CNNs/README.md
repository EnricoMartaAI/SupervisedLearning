To improve the performance of a given CNN for image classification on the CIFAR10 dataset, I have systematically modified its structure and parameters. Below, I outline the changes made, followed by a summary of the best results achieved.

1) Number of Layers
I increased the number of convolutional layers up to five, varying the number of filters, input, and output channels. The best accuracy achieved through this modification was 63%, indicating some improvement, but the loss remained high, around 1. I also experimented with padding to better recognize boundaries and to add more convolutional layers by controlling image dimensions more effectively. Additionally, I incorporated Local Response Normalization (LRN) in the first two layers to enhance edge and texture recognition. However, this led to a decrease in accuracy to 59%, with the loss remaining almost unchanged.

2) Number of Epochs
Given the previous results, I increased the number of epochs up to 10 to improve the model's training and performance. I tested the CNN both with and without LRN. In the first case, the accuracy reached 75% with a loss of 0.25, while in the second, the accuracy was 74% with a loss of 0.19. Although the results showed improvement, they did not fully meet my expectations.

3) Learning Rate
To reduce the loss, I experimented with different learning rates, initially increasing it from 0.001 to 0.01. However, this caused the accuracy to drop to 10%, prompting a change in strategy. I then implemented an adaptive learning rate, adjusting it gradually (starting from 0.01 and dividing by 0.8 every two steps) to ensure continuous loss reduction and enhance model stability. I also switched to the Leaky ReLU activation function to avoid vanishing gradients. Along with LRN, these changes resulted in an accuracy of 76% and a loss of approximately 0.14.

4) Dropout
Given the high number of parameters, which risked leading to overfitting, I implemented Dropout. This further refinement aimed to stabilize the model and prevent overfitting.
