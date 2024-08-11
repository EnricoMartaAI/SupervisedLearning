Introduction:
My objective is to use different recurrent neural network (RNN) architectures to predict the last character of a given sentence. 
I am using the book "Alice's Adventures in Wonderland" as the dataset. 
I have preprocessed the text by converting all characters to lowercase and replacing non-alphanumeric characters and newline characters with spaces, ensuring that the text contains only letters and spaces. 
The goal of my neural network is to recursively complete the last word of an extracted sentence, enabling the generation of entire sentences.

Models:
The models I used are:
RNN (Recurrent Neural Network): The most general form of recurrent neural networks.
LSTM (Long Short-Term Memory): A variant of the basic RNN, capable of learning long-term dependencies. 
It includes mechanisms called gates—specifically, the input gate for adding information to the cell state and the forget gate for removing information.
GRU (Gated Recurrent Unit): A simplified version of the LSTM, combining the input and forget gates into a single update gate, reducing complexity and improving model efficiency.

Changes:
I started with LSTM, using the following parameters:
Hidden Dimension: 256
Number of Layers: 2
Dropout: 0.5
Learning Rate: 0.01
Patience: 8

Initially, I observed that the primary objective of the model—to predict the subsequent character—was met.
The model was also capable of constructing meaningful words.
However, after generating a few words, the model tended to get stuck in a loop. 
For example, given a prompt, the model produced repetitive sequences after a certain point.

I then changed the number of layers from 2 to 4 to see if there was any improvement, but there were no significant changes, even though the best loss decreased slightly, from 2.2696 to 2.1518.

When I increased the number of layers to 10, I noticed that the model could no longer predict words; 
it only predicted spaces. 
This issue might be due to the high prevalence of space characters in the text, leading to overfitting because all non-standard characters were converted to spaces during preprocessing.

Next, I adjusted the dropout rates from 0.2 to 0.5 and then to 0.7. 
Again, I didn’t observe any significant changes, although it seemed to slightly increase the training percentage.

I also altered the dimension of the hidden state, both increasing and decreasing it. 
However, these modifications did not lead to any improvements in the results. 
Then, I adjusted the learning rate by reducing it and implementing an adaptive approach. 
Finally, I modified the patience parameter to allow for extended training periods, but still, there were no observable changes.

I applied similar modifications to the other two models. 
I noticed that the training process of LSTM is quite a bit longer than that of GRU, and significantly longer than that of RNN. 
The differences in training times are due to the significant difference in the number of parameters among the different network architectures.

Here’s a comparison:

RNN: 0.7795 minutes per epoch (20 epochs)
GRU: 1.6415 minutes per epoch (13 epochs)
LSTM: 1.9871 minutes per epoch (14 epochs)
This difference is due to the number of parameters in each network.
I also observed variations in speed by changing the network structure, such as increasing the number of layers and reducing the size of the hidden state. 
These changes allowed an increase in the number of epochs actually executed, thus letting the loss function achieve better results.

In conclusion, to prevent looping, I manually inserted a character or an entire word into the sequence to observe the model's reaction. 
Even though this approach sometimes stopped the loop, the model would eventually start looping again after a while.
