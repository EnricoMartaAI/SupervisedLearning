Introduction:
My task is to train a Transformer model to take an input sequence and generate the output sequence with the elements in reversed order. 
Initially, I tested the model on sequences of numbers that were 16 elements long. Both the validation and test errors were 0%, meaning the model achieved 100% accuracy.
I also printed the attention map, which clearly showed that the model learned to focus on the token that corresponds to the reversed index of itself. 
Although there was some noise for nearby positions, the exact positions still dominated.
Next, I increased the sequence length to 50 to observe how the model's performance might degrade. 
I also expected to see an increase in training times, as discussed in class: "when the sequence length exceeds the hidden dimensionality, self-attention becomes more expensive."

Evaluations:
The model continued to achieve high accuracy in both validation and test phases, maintaining 100% accuracy. There was no degradation in performance.
The key parameter to watch is the color intensity in the attention map, which indicates the strength of the attention weights. 
As expected, the positions with brighter colors are on the diagonal.
Even though the attention map shows very little noise, it is negligible compared to the intensity of the colors on the diagonal.
However, I decided to further increase the sequence length to see when the model's accuracy would start to decline. 
At a sequence length of 150, both the validation and test accuracy dropped to 94%.
