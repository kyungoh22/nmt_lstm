This is Part 1 of my three-part Neural Machine Translation project. 

Here in Part 1, I create a model based on LSTMs. 

Model Architecture

Encoder

The Encoder comprises a series of LSTM units. The source sentence is passed through an Embedding layer (with pre-trained weights), before being fed to the series of LSTM units. The Encoder outputs the final hidden state and cell state vectors, which together represent the entire input sentence. 

Decoder

The Decoder also comprises a series of LSTM units. We use the Encoder's final hidden and cell states as the Decoder's initial hidden and cell states. 

Training and Inference

Training

We use teacher forcing to train our model. This means we compute the loss by comparing the ground-truth target output at time-step t with the prediction at time-step (t-1). 

Inference

Once the model's weights have been optimized during the training, we can start making predictions. First, we pass the source sentence into our Encoder to obtain the Encoder's final hidden state and final cell state. These two vectors alone represent the entire source sentence. The two state vectors are then passed into the Decoder as its initial states. The inference process takes place one time-step at a time. For each LSTM unit in the Decoder, we feed in the prediction from the previous time-step as the input, along with the hidden and cell states from the previous time-step. This iterative process continues for the pre-defined maximum number of steps, or until an LSTM unit predicts the "_END" token.

