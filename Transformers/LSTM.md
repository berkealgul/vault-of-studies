sAs seen in [[Seq2Seq Models]] RNN's have vanising&exploding gradient problem which can be problem with long sequances Long and Short term memory aka LSTM is proposed to tackle this issue.

LSTM solves this problem by introducing long and short term memory. Short term memory is hidden state similar to RRN's, in contrast long term memory, prevents gradients from vanishing

![[LSTM_1.png]]

First stage is called the Forget Gate which determinates what percentage of long term memory will be remembered.

![[LSTM_2.png]]

Second stage is to create new potential long term memory (blue is sigmoid orange is tanh activation function)

![[LSTM_3.png]]

Last stage which is called Output Gate will calculate output(or short term memory) of LSTM unit

![[LSTM_4.png]]