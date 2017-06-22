# seq2seq
## tf.contrib.sequence_loss
sequence_loss(logits, targets, weights,
                  average_across_timesteps=True, average_across_batch=True,
                  softmax_loss_function=None, name=None)
### logits: 
shape [batch_size, sequence_length, num_decoder_symbols], 
* batch_size 指batch大小
* sequence_length 序列长度，指num_steps
* num_decoder_symbols 指输出词库的大小vocab_size
### targets | weights
shape [batch_size, sequence_length]
### 
sequence_loss_by_example的做法是，针对logits中的每一个num_step,即[batch_size, vocab_size], 对所有vocab_size个预测结果，得出预测值最大的那个类别，与target中的值相比较计算Loss值

# tensor board
## Visualizing Learning

## Embedding Visualizing