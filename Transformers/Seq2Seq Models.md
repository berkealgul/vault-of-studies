Used in language translition. It can also reffered as encoder-decoder techique

encoder-decoder consists two seperate networks encoder and decoder.
Deep RRN are usually used.

First input get encoded at encode network, after that we get outputs by putting encoded data into decoder network!

![[seq2seq.png]]

Meanwhile this approach can be powerfull but due to vanishing&exploding gradiant problem learning with long sequances is hard.