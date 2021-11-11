# Music Generation using LSTM
A simple application of a multi-layered LSTM Network to generate original Folk-style music which are aesthetically pleasing for the listener. 

## Overview

Here, we have trained a Many-to-many LSTM Network with musical sequences and the corresponding following note sequences found in the musical notation of a piece composed by an artist. As a result, the Network somehow learns to extract a common 'musical quality' which is preserved in all of the input musical sequences. when we test the network completely random sequence inputs, the network returns quite interesting and aeshetically pleasing original musical pieces which are completely machine-generated. 

## Training and Model Architecture

There are 86 unique chaaracters in the ABC notation of the musical sequences used as training data for the LSTM Network. A sequence of 64 such characters is used to contruct each of the input sequence used in the training process. To speed up the training process, we train the architecture with batches of 16 input sequences. 

The first layer of the architecture is an Embedding layer which maps every input sequence into a 512-dimensional vector. This is followed by a collection of LSTM layers (256 cells each) and Dropout layers. Finally, a 'TimeDistributed' Dense Layer binds the outputs of the LSTM cells in the last layer into a sequence output with Softmax activation. The overall architecture can be clearly seen from the model summary :

<pre>
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
embedding_1 (Embedding)      (16, 64, 512)             44032     
_________________________________________________________________
lstm_1 (LSTM)                (16, 64, 256)             787456    
_________________________________________________________________
dropout_1 (Dropout)          (16, 64, 256)             0         
_________________________________________________________________
lstm_2 (LSTM)                (16, 64, 256)             525312    
_________________________________________________________________
dropout_2 (Dropout)          (16, 64, 256)             0         
_________________________________________________________________
lstm_3 (LSTM)                (16, 64, 256)             525312    
_________________________________________________________________
dropout_3 (Dropout)          (16, 64, 256)             0         
_________________________________________________________________
time_distributed_1 (TimeDist (16, 64, 86)              22102     
_________________________________________________________________
activation_1 (Activation)    (16, 64, 86)              0         
=================================================================
Total params: 1,904,214
Trainable params: 1,904,214
Non-trainable params: 0
_________________________________________________________________
</pre>
