Introduction:
My goal in this laboratory is to train a model to recognize the number on Uno cards in an image and to locate the number in the top-left corner of each card. 
To achieve this, I implemented a Faster R-CNN model that was previously trained on the COCO-V1 dataset.
To evaluate the effectiveness of my model, I used the Intersection over Union (IoU) metric to measure how accurately the predicted bounding boxes overlap with the ground truth. 
This allows me to estimate the model's ability to correctly locate the target objects.
At the end of this report, I provide comments on the results, making assumptions about why some cards were not recognized correctly while others were.

Data Preprocessing:
I used data augmentation to make the model more robust by mimicking different image conditions. 
Randomly, I implemented the following techniques:
Horizontal flip
90-degree rotations
Blurring effects

Results:
I only trained the model for one epoch. Here are the results:
Train Loss: 0.349
Validation Loss: 0.159
Time: 11.827 minutes

Now, I will review the results from the worst to the best, analyzing each case individually.

IoU = 0.5608: This image had the lowest IoU score observed.
The model failed to recognize one of the three cards, specifically the number 6, which is the least visible. 
The card is partially occluded by another card, which likely explains the poor performance.

IoU = 0.5666: In this case, the unrecognized card is the most visible of the two, but it is again the number 6. 
I suspect that the model was not adequately trained to recognize the number 6, or perhaps the cards are in an unusual orientation, making object detection difficult. 
Additionally, the image is particularly blurred.

IoU = 0.6049: Here, the problem is that the "Skip Turn" card is particularly obscured by another card.

IoU = 0.9438: This image had the highest IoU score. The background is not particularly challenging, the resolution is very high, and the cards are well spaced.
As a result, the model performed well.

IoU = 0.8371: This is an intermediate case. 
The cards that might be more challenging to recognize are "+2" and "+4", yet the model does a good job. 
The "4" in "+4" is slightly obscured, but the black background and the "+" sign likely helped the model.

Conclusion:
I observed that various factors can contribute to the deterioration of model performance in different images.
The most significant factor is occlusion, where objects are partially or completely obscured by other elements. 
In addition, low resolution or blurring can significantly hinder accurate object detection.
I also believe that object orientation can complicate the detection process. This could likely be mitigated through data augmentation.
