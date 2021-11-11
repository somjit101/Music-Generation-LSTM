# Music Generation using LSTM
A simple application of a multi-layered LSTM Network to generate original Folk-style music which are aesthetically pleasing for the listener. 

## Overview

Here, we have trained a **Many-to-Many LSTM Network** with musical sequences and the corresponding following note sequences found in the musical notation of a piece composed by an artist. As a result, the Network somehow learns to extract a common **'musical quality'** which is preserved in all of the input musical sequences. When we test the network with completely random sequence inputs, the network returns quite interesting and aeshetically pleasing original musical pieces which are completely machine-generated. 

## Training and Model Architecture

There are **86 unique chaaracters** in the ABC notation of the musical sequences used as training data for the LSTM Network. A **sequence of 64 such characters** is used to contruct each of the input sequence used in the training process. To speed up the training process, we train the architecture with **batches of 16 input sequences**. 

The first layer of the architecture is an Embedding layer which maps every input sequence into a **512-dimensional vector**. This is followed by a collection of LSTM layers (**256 cells each**) and Dropout layers. Finally, a **'TimeDistributed'** Dense Layer binds the outputs of the LSTM cells in the last layer into a sequence output with Softmax activation. The **overall architecture** can be clearly seen from the model summary :

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


## The Dataset 

We have used the [Nottingham Music Database](http://abc.sourceforge.net/NMD/) in [**ABC notation**](https://en.wikipedia.org/wiki/ABC_notation) which contains over 1000 folk tunes.

## Usage 

All input data should be placed in the [data](data/) directory. The example [input.txt](data/input.txt) is taken from the [Nottingham Dataset (Cleaned)](https://github.com/jukedeck/nottingham-dataset).

To train the model with default settings:
```bash
$ python train.py
```

To sample the model:
```bash
$ python sample.py 100
```

Training loss/accuracy is stored in [training_log.csv](logs/training_log.csv).

Also, to prevent the loss of intermediate weights during the training epochs of the model, the weights are saved in the [model](model/) directory. The training process can take a significant amount of time. 

## References 

* [Karpathy's Implementation of Character-RNN](https://github.com/karpathy/char-rnn)
* [The effectiveness of RNNs by Karpathy](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
* [MIDI Music Generation](https://towardsdatascience.com/how-to-generate-music-using-a-lstm-neural-network-in-keras-68786834d4c5)  &rarr;  [Source Code](https://github.com/Skuldur/Classical-Piano-Composer)
* [Generating Tabla Music Part 1](https://www.trivedigaurav.com/blog/machines-learn-to-play-tabla/)
* [Generating Tabla Music Part 2](https://www.trivedigaurav.com/blog/machines-learn-to-play-tabla-part-2/)
* [RNN-composed Tabla Long Composition](https://soundcloud.com/trivedigaurav/char-rnn-composes-long-composition)
* [NN for Generating Music - Surveyed Blog](https://medium.com/artists-and-machine-intelligence/neural-nets-for-generating-music-f46dffac21c0)
* [FolkRNN Irish Folk Music Generator](https://folkrnn.org/)
* [RNN-composed Piano Music](https://soundcloud.com/sigur-ur-sk-li/neuralnet-music-1)
* [Google Magenta](https://magenta.tensorflow.org/)
* [ABC to Sheet Music Converter](https://www.abcjs.net/abcjs-editor.html)
