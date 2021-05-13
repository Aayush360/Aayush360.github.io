# Attention!


After going through the development timelines of sequence model, I encountered with the concepts of RNN, LSTM, GRU, Transformers ...
Prior to this, I have acquired some intutition about image data, one of the popular and widely generated unstructured data out there.
I came to know how CNN is used to capture the spatial relationship in images using the concpets of mask/kernel using bunch of linear and non-linear functions.

But when it comes to text and speech data, which inherently contains temporal relationship (relating to time) CNN  performs poorly.
Thus, to capture the temporal relationships in text corupus and make sense out of it, we have a completely different architecture called Recurrent Neural Network
(RNN). The intuition is, instead of taking only the activation of prior layer (hidden state) we also take output from the previous layer so as to remember better.

But taking only the output of previous layer may not perform at well, thus RNN cannot remember long sentences. To build upon this, they introduced concepts of
LSTM (Long short term memory) that uses complex architecture with gates like: Input, Update and Forget gate so as to capture the temporal relationships better.
A simplified version of LSTM was later introdued called Gated Recurret Unit, which is simpler than LSTM in architecture and has only 2 gates instead of 3.

But even LSTM and GRU failed in memorizing very long sentences. That is when the concept of Attention model came into picture. 
I read somewhere that Attention is just a fancy name for weighted average, indeed it is.

Let me explain it in less-mathy way the best I could:

Consider the sentence: **The FBI is chasing ......**
where, chasing is target word for us and the words The, FBI, and is is the input word.

Here we want to calculate the attention of target word (chasing) with respect to input words (The, FBI, is). That is, how much attentin should the input words (words closer to the target
words in a sentence) pay to determine the output word ? 
For this probelem, we represent each word in 3 vectors: Key vector, Value vector and Query vector.

If we want to calculate the attention of output word chasing, find the similarity of word FBI with other 3 words. To do this we use dot-product as similariy measure.
We can use other similariy measures as well like cosine, euclidean distance etc. 

The dot product between Query vector for chasing with Key vectors of other 3 words gives us the similarity measure. Now, we use softmax activation to convert
these similarity measure into probabiliy distribution.

The value vector for the 3 words is taken to take weighted average for the target word, where weights are the probabilities obtained form the softmax. 
The obtained result is the value for the target word.


The example we have taken here describes self-attention, which is specific to same sentences.
Since we are computing the attention of each word to other words of the same sentence - this is called self- attention.

**Resources Followed** :(Video lecture from Ali Ghodsi, University of Waterloo) 
youtube.com/watch?v=WFcH7kRNEBc&list=PLehuLRPyt1Hwqk1BopyiREdPfJng2cuNQ&index=7
