# LSTM
nn.embedding: 一个保存了固定字典和大小的简单查找表。这个模块常用来保存词嵌入和用下标检索它们。模块的输入是一个下标的列表，输出是对应的词嵌入
nn.embedding(the len of vacabulary(type is defined as dict), embedding_dim(defined by the complexity of word prediction))
eg. an Embedding module containing 10 tensors of size 3
embedding = nn.Embedding(10, 3)

nn.LSTM (input, hidden, num_layer(default as 1))
hidden can be the sequece number of data. (how many sentences do u have)

output ：（seq_len, batch, num_directions * hidden_size）

h_n：(num_layers * num_directions, batch, hidden_size)

c_n ：（num_layers * num_directions, batch, hidden_size）

eg.
import torch.nn as nn
import torch
x = torch.rand(24,10,100) #seq,batch,input_size
h0 = torch.rand(1,10,16)# num_layers*num_directions, batch, hidden_size      bidirectional=True,num_directions=2,otherwise１
c0 = torch.rand(1,10,16)

lstm = nn.LSTM(100,16) 16 is hidden size, 100 is input size

h_0是格式为(num_layers * num_directions, batch, hidden_size)的tensor 它包含batch中每个元素的最初的隐态.若为双向lstm num_dire…=2 否则=1
c_0是格式为(seq_len, batch, input_size）的tensor 它包含batch中每个元素最初的cell state.  若h_0和c_0不提供，则默认为h_0 and c_0 valued as 0.



output,(h,c) = lstm(x,(h0,c0))
output.shape-----torch.Size([24, 10, 16])
c.shape----------torch.Size([1, 10, 16])
h.shape----------torch.Size([1, 10, 16])

h_n是形状为(num_layers * num_directions, batch, hidden_size)的tensor， 包含t=seq_len（即序列末尾）的隐态值
c_n是形状为(num_layers * num_directions, batch, hidden_size)的tensor， 包含t=seq_len（即序列末尾）的cell值
