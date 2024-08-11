Introduction
Given a dataset containing ages and genders of individuals, along with images of their faces, my objective is to predict the exact age associated with each individual's face. For my analysis, I used algorithms such as MobileNet V2 and GoogLeNet, both of which were pre-trained on the ImageNet1K-V1 dataset. I adapted these algorithms to achieve my goal.

The Models
In both models, I modified the final layers (classifier) for two reasons. The first reason is that the original models were designed to classify 1000 classes, whereas my goal is to perform regression. The second reason is that I wanted the last layers to be fine-tuned for my dataset, utilizing transfer learning.

Initially, I allowed only the last layers to be trainable. Later, I allowed the entire neural network to be trained. I divided the dataset into training, validation, and test sets. Throughout the training process, I used the validation set at the end of each epoch to evaluate the effectiveness of the training. To assess the overall quality of the training and the model, I used Pearson and Spearman correlation coefficients to measure the relationship between predicted and actual values.

Performance
I first present the results of the original model with only the last parameters free. As I analyzed the results, I observed that the points were more condensed in the left part of the graph, suggesting that the algorithm tended to associate lower ages than the actual ones. This observation was confirmed by the SROCC and PLCC values.

Next, I compared these results with those from the model where all parameters were free to be adjusted. It’s important to note that this model adjusted all 59,209,345 parameters instead of just 1,065,537. The increase in PLCC and SROCC values during training suggested that the model was becoming more accurate over time. Moreover, these results were consistent with the metrics applied to the validation test, indicating that there was no overfitting.

When I switched to GoogLeNet, I followed the same process as before. Initially, I limited the number of free parameters. Then, I allowed all parameters to be free. I observed a similar behavior to the previous CNN, but GoogLeNet achieved slightly better results. Additionally, this model had a lower computational cost, as GoogLeNet has 6,141,153 parameters. I noted that I reported only the results from the best-performing CNN among those I implemented.
